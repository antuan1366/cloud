# AWS Cost and Cleanup Controls

Last updated: 2026-10-31

## Account context — user-reported, recheck live
- AWS Credits page previously showed USD 120 remaining.
- Console message previously said access/free access ends on 2026-11-05 or when credits are depleted.
- Current balance, service eligibility, usage, billing, and exact account terms are not freshly verified.
- User may be an IAM user rather than account owner; billing visibility may be restricted.

## Mandatory pre-deployment gate
Before creating or enabling any AWS resource:
1. Verify current credit balance, expiry, eligible services, account terms, and Region.
2. Check current usage/billing and inspect existing resources, especially the previous Terraform-managed EC2 lab.
3. List every resource and dependency the action will create.
4. Check current official pricing for exact Region, size, runtime, storage, public IP, data transfer, requests, and dependent services.
5. Explain charges while running, stopped, or idle.
6. Explain exact cleanup steps, including resources not removed automatically.
7. Present estimates as estimates, not guarantees.
8. Obtain explicit user approval.

## Cost risks
- Linux EC2 runtime (proposed t3.medium).
- Windows EC2 runtime and Windows licensing.
- Amazon RDS compute, storage, backups, snapshots, and retained storage after stopping/deletion.
- EBS volumes and snapshots.
- Public IPv4 addresses and data transfer.
- Application Load Balancer hourly and capacity-unit charges.
- AWS WAF Web ACL, rules, and request charges.
- S3 storage, requests, and data transfer.
- CloudWatch logs/metrics/alarms beyond applicable allowances.
- GuardDuty, Security Hub, Inspector, AWS Network Firewall, NAT Gateway, and third-party virtual appliances.
- Microsoft Remote Desktop Services CAL/licensing requirements are separate from AWS compute estimates.

## Stop/delete behavior
- Stopping EC2 stops compute billing but EBS storage continues. Public IPv4 charges may also apply depending on address allocation and current pricing.
- An EC2 stop/start can change its automatically assigned public IPv4 address.
- Stopping RDS does not stop storage and backup charges. AWS automatically starts an RDS instance after seven consecutive days stopped.
- ALB continues charging independently of EC2 target state; delete it when not needed.
- WAF charges can continue while its Web ACL remains deployed/associated; remove unused resources after checking dependencies.
- NAT Gateway and AWS Network Firewall can continue hourly charges even when workload EC2 instances are stopped; delete when not in use.
- S3 storage/requests can continue to incur charges until objects/bucket are removed.
- EBS snapshots and retained RDS backups can continue to incur charges after compute deletion.
- Budget alerts are notifications, not hard spending caps; billing data can be delayed.
- Promotional credits may exclude some services.

## Cost-saving approach
- Deploy only resources needed for the current day's exercise.
- Stop Linux and Windows EC2 after use, checking storage/IP implications.
- Stop RDS after its exercise; remember the seven-day auto-start and retained storage charges.
- Create ALB/WAF only for their exercise; delete afterward.
- Avoid NAT Gateway and AWS Network Firewall in the base lab unless separately approved.
- Avoid leaving paid managed services running overnight.
- Use two Docker containers on one host rather than a second app EC2 for the initial exercise.
- Keep S3 test data small and delete it if no longer needed.

## Cleanup checklist
Before: save required docs/evidence; confirm data can be discarded; identify lab resources by tags/names/IDs/Region; identify dependencies; obtain approval.
During: delete temporary ALB/WAF and other hourly-billed resources when no longer needed; stop/delete EC2/RDS according to retention decision; remove unused public IPs; review EBS volumes/snapshots, AMIs, S3 objects, RDS backups, logs, NAT, and firewall endpoints.
After: inspect all relevant Regions; confirm no unintended resources remain; recheck billing/credits after data updates; record results.

Never delete shared or unrelated resources. Never assume stopping an instance is complete cleanup.
