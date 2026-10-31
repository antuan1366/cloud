# Runbook

Status: revised for the Console-first six-day lab. No new resources are approved for deployment by this document.

## Operating rules
- Use AWS Management Console for infrastructure configuration in this iteration.
- Do not use Terraform or AWS CLI to deploy this environment.
- Terminal commands inside EC2 may be used for Docker/OS configuration; explain commands and side effects first.
- Check current prices and credit eligibility before each potentially billable action.
- Obtain explicit approval before resource creation or paid service activation.
- Inspect existing resources before adding new ones.

## Before Day 1
1. Select the correct AWS account and Region.
2. Review current credit balance, expiry, eligible services, usage, and billing visibility.
3. Inspect the previous Terraform-managed EC2 lab and related resources.
4. Confirm whether to retain or remove the previous lab; never delete without approval.
5. Review current prices and resource dependencies.
6. Record the VPC CIDR and subnet map.

## Console workflow — network
1. Open VPC service.
2. Create VPC and enable DNS support/hostnames if needed.
3. Create public, application, database, and management subnets across intended AZs.
4. Create and attach Internet Gateway.
5. Create route tables and associate subnets deliberately.
6. Create Security Groups for ALB, app EC2, RDS, and Windows management.
7. Create NACLs only with a clear stateless rule plan; include return/ephemeral traffic.
8. Verify routes and access paths before launching compute.

## Console workflow — application
1. Launch one Linux EC2 into the intended private application subnet.
2. Choose a secure management path before launch; avoid unrestricted SSH.
3. Install Docker.
4. Deploy two application containers and one HAProxy or Traefik container.
5. Test request distribution, container health, logs, and one-container failure.
6. Remember all containers share one EC2 failure domain.

## Console workflow — Amazon RDS and S3
1. Create DB subnet group using private subnets in two AZs.
2. Launch PostgreSQL Single-AZ with Public access disabled and encryption enabled.
3. Restrict inbound PostgreSQL to the application Security Group/source.
4. Create a dedicated least-privilege app DB user.
5. Create a private S3 bucket with encryption and restrictive policy; enable versioning if useful.
6. Test denied access and object recovery.

## Console workflow — Windows / Microsoft RDS
1. Review Windows instance pricing and Microsoft RDS licensing/CAL requirements.
2. Select a secure access path to the private Windows host.
3. Launch one Windows Server EC2.
4. Configure only the Microsoft RDS role(s) needed.
5. Review Windows logs and session policies.
6. Do not claim production HA from one server.

## Console workflow — ALB and WAF
1. Check ALB/WAF pricing and credit eligibility.
2. Create ALB in two public subnets.
3. Configure target group and health checks.
4. Register the app EC2 target.
5. Create/associate WAF Web ACL and selected managed rules.
6. Test with safe requests and inspect metrics/logs.
7. Delete ALB/WAF resources after the exercise if no longer needed.

## Monitoring and assessment
- Use CloudTrail Event History for AWS API activity review.
- Use CloudWatch for metrics/logs/alarms; check log retention and charges.
- Review GuardDuty, Security Hub, and Inspector pricing before activation.
- Prowler, Checkov, and Trivy are separate assessment tools, not all native Console features. Review permissions and scope before running.

## Cleanup
- Stop EC2/RDS only after confirming data-retention needs.
- Delete hourly-billed resources such as ALB, NAT Gateway, and Network Firewall when no longer needed.
- Review EBS volumes, snapshots, public IPv4 addresses, S3 objects, RDS snapshots/backups, and CloudWatch logs.
- Verify all relevant Regions.
- Recheck billing after usage data updates.
- Never delete unrelated or shared resources.
