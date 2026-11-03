# Latest Session Handoff

Date: 2026-11-03
Session: AWS infrastructure and WAF milestone update; Network Firewall postponed
Status: Core network, compute, ALB/HTTPS, RDS, S3, Flow Logs, and WAF exercises are deployed and tested. Network Firewall access blocked before creation.

## User goal
Build practical Cloud Security Engineering capability through a cost-controlled AWS lab in us-east-1. User prefers direct, step-by-step guidance and requires cost warnings before new potentially billable resources. Do not update this repository unless explicitly asked; this session's update was explicitly requested.

## Deployed and tested
- VPC secure-cloud-lab-vpc (10.10.0.0/16), eight workload subnets across us-east-1a/b, IGW, route tables, custom NACLs, and tier-specific SGs.
- No NAT Gateway.
- Private Amazon Linux 2023 EC2 secure-app-server-01, t3.small, App-A private IP 10.10.11.85, no public IP.
- Docker and nginx-app container running nginx:alpine, host port 8080 -> container port 80.
- Session Manager administration through EC2-SSM-Role and SSM/ssmmessages interface endpoints; no SSH.
- Internet-facing ALB secure-cloud-lab-alb in Public-A/B. Target group app-target-group forwards to EC2:8080 and target was Healthy.
- HTTPS 443 listener works; HTTP 80 redirects to HTTPS. ACM certificate is self-signed and browser trust warning is expected; not production-trusted.
- Private Single-AZ RDS PostgreSQL secure-cloud-postgres, Publicly accessible No; app-to-DB port 5432 connectivity and login verified. Do not record DB password. Dedicated app DB user/database not yet created.
- Private S3 bucket secure-cloud-lab-storage-adel-2026, Block Public Access, Bucket owner enforced, SSE-S3. S3 read-only IAM exercise and denied upload verified.
- S3 Gateway Endpoint secure-cloud-s3-endpoint associated with application-route-table; EC2 successfully downloaded the Nginx image from private S3.
- App-A VPC Flow Logs delivered to CloudWatch Logs group /aws/vpc/secure-cloud-lab; REJECT record observed.
- AWS WAF Web ACL secure-cloud-lab-waf associated with ALB; logging to aws-waf-logs-secure-cloud-lab. SQL injection query test was blocked by AWS-AWSManagedRulesSQLiRuleSet / SQLi_QUERYARGUMENTS and logged.
- User reviewed managed/custom WAF rule groups and elected to leave configuration unchanged.

## Network Firewall attempt — blocked
- User selected a one-AZ learning exercise.
- User created firewall-subnet-a, 10.10.41.0/24, us-east-1a.
- Opening VPC > Network Firewall > Firewalls and Firewall Policies returned an error described as “The AWS Access Key Id needs a subscription for the service”.
- No firewall policy or firewall was created. Do not say Network Firewall is deployed or incurring firewall endpoint charges.
- Do not modify routes. Diagnose service access/account/permission restrictions only if user later wants to resume.
- A one-AZ firewall endpoint would not provide complete inspection coverage for this two-AZ environment; route design needs a contained test path.

## Important caveats
- The ALB is billable and remains deployed unless user removes it.
- WAF charges may continue while Web ACL remains deployed/associated.
- RDS, EC2, EBS, CloudWatch Logs, S3, public IPv4, and interface endpoints may incur charges.
- Stopping EC2 does not stop EBS storage charges; ALB/WAF/RDS/endpoints have independent lifecycle/cost.
- Previously reported USD 120 credits and 2026-11-05 access deadline are stale/user-reported; recheck live status.
- Earlier separate Terraform/Ansible t3.micro lab instance is historical and not freshly inventoried.

## Current progress estimate
The assistant previously estimated approximately 70–72% of the broader learning roadmap complete. This is a rough scope estimate, not a measured metric. Network Firewall is postponed; Windows/RDS, VPN, Terraform/Ansible automation, SOC/OpenSearch, resilience testing, full validation, and cleanup remain.

## Suggested next work
1. Check current AWS billing/credits and inventory before further paid work.
2. Decide whether to validate the current architecture or begin Terraform representation of the deployed resources. Terraform should initially be format/validate/plan only; no apply/import/destroy until state and impact are reviewed.
3. Keep OpenSearch and Windows/VPN exercises separate until their costs and scope are agreed.

## Security and handoff rules
- Never ask for passwords, access keys, MFA codes, or private keys.
- Never commit DB passwords, private keys, credentials, or sensitive raw logs.
- Distinguish verified console/test results from user-reported information and plans.
- Give one small next step at a time and explain why it matters.
- Cost review and explicit approval are required before new potentially billable resources.
