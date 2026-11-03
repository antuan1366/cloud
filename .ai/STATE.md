# Current State

Last updated: 2026-11-03
Status: Core AWS network, compute, database, storage, load-balancing, monitoring, and WAF exercises deployed and tested. AWS Network Firewall postponed due account/service-access error.

## Current environment
- Region: us-east-1 (N. Virginia).
- VPC: secure-cloud-lab-vpc, ID vpc-0e64a6406a119a7b0, CIDR 10.10.0.0/16.
- DNS resolution and DNS hostnames enabled; IPv6 disabled.
- Eight workload subnets across us-east-1a and us-east-1b:
  - Public-A 10.10.1.0/24; Public-B 10.10.2.0/24.
  - App-A 10.10.11.0/24; App-B 10.10.12.0/24.
  - DB-A 10.10.21.0/24; DB-B 10.10.22.0/24.
  - Management-A 10.10.31.0/24; Management-B 10.10.32.0/24.
- Dedicated Network Firewall learning subnet was created by user: firewall-subnet-a, 10.10.41.0/24, us-east-1a. No Network Firewall or firewall policy was created.
- Internet Gateway attached. Public route table routes 0.0.0.0/0 to IGW. Application, database, and management routes are private; no NAT Gateway.
- Custom subnet NACLs configured for public, application, database, and management tiers. NACLs are stateless; preserve return/ephemeral-port rules.
- Security Groups: alb-sg, app-sg, db-sg, ssm-endpoint-sg. App ingress TCP 8080 from ALB SG; DB ingress TCP 5432 from app SG; SSM endpoint ingress TCP 443 from app SG.
- Do not assume firewall-subnet-a is associated with a route table or integrated into traffic flow.

## Compute and application
- EC2 secure-app-server-01: Amazon Linux 2023, t3.small, private IP 10.10.11.85 in App-A, no public IP, app-sg, IAM profile EC2-SSM-Role.
- Root EBS: 20 GiB gp3, encrypted, Delete on termination enabled.
- Docker installed and running. Container nginx-app uses nginx:alpine, host TCP 8080 to container TCP 80. This is the actual deployed lab state; it supersedes the earlier proposed no-Nginx/HAProxy-or-Traefik design.
- Nginx image transferred from private S3 bucket; image loaded locally on EC2.
- EC2 administration via Systems Manager Session Manager; no SSH key or inbound TCP 22.
- IAM role EC2-SSM-Role has AmazonSSMManagedInstanceCore. SSM and ssmmessages interface endpoints are in Management-A, private DNS enabled.
- STS call from EC2 timed out because no STS endpoint/NAT route; no STS endpoint created.

## ALB and TLS
- Internet-facing ALB secure-cloud-lab-alb in Public-A/Public-B, DNS: secure-cloud-lab-alb-1576382375.us-east-1.elb.amazonaws.com.
- Target group app-target-group forwards HTTP to EC2 port 8080; target secure-app-server-01 was Healthy.
- HTTPS 443 listener forwards to target group; HTTP 80 redirects to HTTPS 443.
- ACM certificate is self-signed, matches ALB DNS name, and is not publicly trusted. Browser trust warning is expected; curl.exe -k was used for lab testing only. Replace with trusted CA certificate/domain for production.
- ALB is a billable managed service. One registered EC2 target does not provide application HA.

## Database
- RDS PostgreSQL instance secure-cloud-postgres, Available, Single-AZ, private, Publicly accessible = No.
- DB subnet group secure-db-subnet-group includes DB-A and DB-B.
- db-sg permits TCP 5432 from app-sg only.
- PostgreSQL client 15.19 installed on EC2; EC2-to-RDS connectivity verified and user successfully connected.
- Master username dbadmin; password is deliberately not recorded here. Dedicated application DB user/database not yet created.

## S3 and IAM exercise
- Private bucket secure-cloud-lab-storage-adel-2026 in us-east-1; Block Public Access enabled, Bucket owner enforced, SSE-S3 default encryption, versioning disabled.
- Object access anonymous request returned 403 as expected.
- s3-test-user has custom S3-Lab-ReadOnly-Policy: ListBucket and GetObject only; upload denied as expected. User cannot list all buckets because ListAllMyBuckets was not granted.
- S3 Gateway Endpoint secure-cloud-s3-endpoint (com.amazonaws.us-east-1.s3), associated with application-route-table. Endpoint policy is full access for this lab; bucket/IAM policies still govern access.
- EC2 role inline policy S3-Download-Nginx-Lab-Image grants GetObject only on the lab image object. Download and docker load succeeded.

## Monitoring and WAF
- VPC Flow Logs for App-A subnet, destination CloudWatch Logs group /aws/vpc/secure-cloud-lab, Filter All, one-minute aggregation.
- Verified REJECT flow-log record from EC2 to an S3 public endpoint address; user is reviewing logs independently.
- AWS WAF Web ACL secure-cloud-lab-waf associated with secure-cloud-lab-alb in us-east-1.
- WAF log group: aws-waf-logs-secure-cloud-lab.
- SQL injection test URL was blocked by AWS-AWSManagedRulesSQLiRuleSet, rule SQLi_QUERYARGUMENTS; log showed SQL_INJECTION on query argument id.
- Another observed block came from AWS-AWSManagedRulesAnonymousIpList / HostingProviderIPList.
- User reported managed rule groups: CommonRuleSet, SQLiRuleSet, AnonymousIpList, AmazonIpReputationList, AntiDDoSRuleSet. Custom rules reported: GeoRule, GlobalRateBasedRule, RateBasedRuleGET, RateBasedRulePOST, BodySizeRestrictionRule. User-reported WCU total 1,042. Do not assume every listed rule's action without rechecking.
- WAF rule configuration left unchanged after review.

## Network Firewall — postponed
- User chose a one-AZ learning exercise and created firewall-subnet-a (10.10.41.0/24, us-east-1a).
- Opening VPC > Network Firewall > Firewalls and Firewall Policies returned an account/service-access error: “The AWS Access Key Id needs a subscription for the service” (user-reported wording).
- No policy or firewall was created. Do not claim Network Firewall is deployed or billing.
- Resume only after diagnosing account access/subscription/permissions; do not change routes or create a firewall until access is resolved and routing design/cost is reviewed.

## Historical previous lab
- A separate earlier Terraform/Ansible t3.micro EC2/Nginx lab existed (historical instance ID i-05cd787404265bc18; public IP 54.163.28.219). Its current state is not freshly verified. Do not assume it is active or delete it without explicit approval.

## Local tooling — previously verified
- Ubuntu 24.04.5 LTS VM; Git 2.43.0; Terraform 1.17.0; AWS CLI 2.38.6; Python 3.12.3.
- Ansible core 2.21.5 in /home/antuan/ansible-venv.
- Tools are for local learning. Current AWS infrastructure was configured through the Console, not Terraform.

## Account and cost context — user-reported, stale
- User previously reported USD 120 AWS credits and an access/free-plan deadline of 2026-11-05. These are not freshly verified; recheck live balance, expiry, eligibility, billing visibility, and usage.
- ALB, WAF, RDS, EC2, EBS, S3, CloudWatch Logs, public IPv4, and endpoints may incur charges. No exact current credit balance recorded.
- Network Firewall cost was previously discussed; no firewall resource was created.
- Stopping EC2 does not stop EBS charges. ALB/WAF/RDS and other managed services may continue charging independently.

## Not yet completed
- Windows Server EC2 / Microsoft Remote Desktop Services exercise.
- VPN exercise (type not selected).
- AWS Network Firewall (blocked/postponed).
- Centralized SOC log analytics with OpenSearch (planned, not deployed).
- Terraform infrastructure-as-code reconstruction; Ansible automation; CI/CD.
- Dedicated least-privilege application DB user/database.
- Full security validation, resilience/recovery testing, cost review, and cleanup.
- GitHub architecture diagrams and evidence pack.

## Immediate next actions
1. Review live AWS billing/credits and inventory because previous expiry information is stale.
2. Decide next learning milestone with cost review before creating any new paid resource.
3. Consider Terraform reconstruction of the existing architecture as the next major skill milestone; do not run apply/destroy without explicit scope and approval.
4. Update documentation only when the user explicitly asks.

## Evidence labels
- Verified: confirmed through console/command output in the conversation.
- User-reported: stated by user but not independently verified.
- Planned: intended, not deployed.
- Blocked: unable to proceed pending a specific issue.
