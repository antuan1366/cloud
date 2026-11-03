# Task Backlog

Last updated: 2026-11-03

Status: [ ] not started, [~] in progress, [x] verified complete, [!] blocked. Completion is based on evidence, not intention.

## P0 — Cost, account, and operational safety
- [ ] Recheck AWS credit balance, expiry, eligible services, billing visibility, and current usage.
- [ ] Inventory all resources in relevant Regions; identify any resources still generating charges.
- [ ] Review current charges for EC2, EBS, ALB, WAF, RDS, S3, CloudWatch Logs, public IPv4, and VPC endpoints.
- [ ] Plan cleanup for temporary services; obtain approval before deletion.
- [ ] Do not assume promotional credits cover every service.

## P1 — Existing environment: validation and documentation
- [x] VPC and eight workload subnets across two AZs.
- [x] Internet Gateway and public/private route-table separation; no NAT Gateway.
- [x] Custom NACLs and tier-specific Security Groups.
- [x] SSM Session Manager access without SSH; SSM interface endpoints and EC2 IAM role.
- [x] Private Amazon Linux EC2 with Docker and Nginx container.
- [x] Internet-facing ALB, target group health check, HTTPS listener, and HTTP-to-HTTPS redirect.
- [x] Private Single-AZ PostgreSQL RDS and EC2-to-RDS connectivity.
- [x] Private S3 bucket, encryption, read-only IAM exercise, and S3 Gateway Endpoint.
- [x] App-A VPC Flow Logs delivered to CloudWatch Logs; REJECT record observed.
- [x] AWS WAF associated with ALB; SQL injection test blocked and logged.
- [ ] Create dedicated least-privilege application DB user/database and test application access.
- [ ] Perform a complete security-group/NACL/route review against the intended traffic matrix.
- [ ] Validate trusted TLS certificate path; current ACM certificate is self-signed and unsuitable for production.
- [ ] Test backups/recovery and document limitations.
- [ ] Save sanitized, non-sensitive test evidence.

## P2 — Blocked/postponed network security
- [!] AWS Network Firewall: user created firewall-subnet-a (10.10.41.0/24, us-east-1a), but VPC Network Firewall Firewalls and Firewall Policies pages return an account/service-access error mentioning Access Key Id subscription. No firewall policy or firewall exists.
- [ ] Diagnose account/service access and IAM/organization restrictions before resuming Network Firewall.
- [ ] Revisit routing design before any firewall deployment; do not route all two-AZ traffic through a one-AZ endpoint.
- [ ] VPN exercise: choose Site-to-Site VPN, Client VPN, or self-managed WireGuard/IPsec after scope/cost review.

## P3 — Windows / Microsoft Remote Desktop Services
- [ ] Review Windows EC2 pricing and Microsoft RDS CAL/licensing requirements.
- [ ] Choose secure access to private Windows host; never expose RDP to all sources.
- [ ] Launch Windows Server EC2 only after cost review and approval.
- [ ] Configure minimum RDS roles required for learning.
- [ ] Review Windows security/session logs.

## P4 — Cloud automation and engineering
- [ ] Build Terraform configuration to represent the existing network and security architecture; initially use plan/validation only.
- [ ] Do not import, recreate, apply, or destroy live resources until state strategy and blast radius are reviewed.
- [ ] Use Ansible for repeatable Linux host configuration.
- [ ] Add basic shell/Python operational checks.
- [ ] Add a small CI workflow for formatting, validation, and security checks.
- [ ] Consider container image scanning and IaC scanning after defining safe scope.

## P5 — SOC / centralized log analytics
- [ ] Extend CloudWatch collection to selected WAF, VPC Flow Logs, CloudTrail, and application logs.
- [ ] Review OpenSearch and ingestion architecture/pricing before provisioning.
- [ ] If approved, build searches, field extraction, visualizations, and dashboards.
- [ ] GuardDuty, Security Hub, and Inspector require separate pricing review before activation.

## P6 — Final assessment and cleanup
- [ ] Review IAM least privilege, network paths, encryption, public exposure, logging, and secrets handling.
- [ ] Run selected assessment tools only after scope, permissions, and cost review.
- [ ] Remove temporary ALB/WAF and other resources when no longer needed and approved.
- [ ] Review EBS volumes/snapshots, RDS backups, S3 objects, logs, public IPv4, and endpoints.
- [ ] Verify remaining billable resources across relevant Regions.
- [ ] Recheck billing/credits after usage data updates.
- [ ] Publish architecture diagram, access matrix, test evidence, known limitations, and cleanup record.

## Cost and safety gates
- Explain cost assumptions, runtime, storage/network dependencies, and cleanup before every new potentially billable resource.
- Obtain explicit approval before provisioning or enabling paid resources.
- AWS infrastructure has been configured through the Console in this iteration.
- Do not commit credentials, private keys, DB passwords, tokens, or sensitive logs.
- No Network Firewall resource exists; firewall-subnet-a alone does not mean firewall inspection is active.
