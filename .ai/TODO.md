# Task Backlog

Status: [ ] not started, [~] in progress, [x] verified complete, [!] blocked. Mark complete only when acceptance criteria are met.

## P0 — Account safety and existing resources
- [ ] Recheck AWS credit balance, expiry, eligible services, terms, and current usage.
- [ ] Check billing visibility, budgets/alerts, and account permissions.
- [ ] Inspect existing resources in relevant Regions, especially the previous Terraform-managed EC2 lab.
- [ ] Decide whether to retain or remove the previous lab; obtain explicit approval before deletion.
- [ ] Confirm Region and secure administration access.

## P1 — Day 1: VPC and segmentation
- [ ] Create one VPC after cost review and approval.
- [ ] Create public, application, database, and management subnets across two AZs.
- [ ] Configure Internet Gateway and route tables.
- [ ] Create Security Groups for ALB, app EC2, RDS, and Windows management.
- [ ] Create/test NACLs; account for stateless return traffic and ephemeral ports.
- [ ] Record subnet, route table, and access matrix.
- Acceptance: intended traffic works; RDS and app are not directly exposed to the internet.

## P2 — Day 2: Docker application
- [ ] Launch one Linux EC2 t3.medium after cost approval.
- [ ] Install Docker and deploy two application containers.
- [ ] Deploy HAProxy or Traefik as a containerized load balancer (choose one).
- [ ] Configure health checks and test request distribution.
- [ ] Stop one app container and verify remaining behavior.
- Acceptance: app served through Docker proxy; host-level HA limitation documented.

## P3 — Day 3: Amazon RDS and S3
- [ ] Create DB subnet group across private DB subnets in two AZs.
- [ ] Deploy one private Single-AZ PostgreSQL RDS instance after cost approval.
- [ ] Disable public accessibility and enable encryption.
- [ ] Restrict DB ingress to the application Security Group/source.
- [ ] Configure app DB connection with dedicated least-privilege user.
- [ ] Create private S3 bucket; configure encryption, access policy, optional versioning.
- [ ] Test denied access and object recovery.
- Acceptance: app connects to RDS; unauthorized access fails; S3 remains private.

## P4 — Day 4: Microsoft Remote Desktop Services
- [ ] Review Windows EC2 pricing and Microsoft RDS CAL/licensing requirements.
- [ ] Choose secure access to private Windows host; never expose RDP to all sources.
- [ ] Launch one Windows Server EC2 after cost approval.
- [ ] Configure minimum Microsoft RDS role(s) needed for learning.
- [ ] Review Windows security/session logs.
- Acceptance: authorized administration works; unauthorized RDP fails; single-server limitations documented.

## P5 — Day 5: ALB, WAF, firewalling
- [ ] Review ALB/WAF pricing before deployment.
- [ ] Create temporary ALB in two public subnets.
- [ ] Register app EC2 target and configure health checks.
- [ ] Attach AWS WAF Web ACL and selected managed rules.
- [ ] Test safe representative SQLi/XSS requests and inspect metrics/logs.
- [ ] Compare F5 Advanced WAF and FortiWeb conceptually; no licensed appliance deployment without separate approval.
- [ ] Explain AWS Network Firewall/FortiGate-VM placement and cost.
- Acceptance: ALB health and WAF behavior verified; no HA claim from one target.

## P6 — Day 6: monitoring, assessment, cleanup
- [ ] Review CloudTrail Event History and CloudWatch.
- [ ] Review GuardDuty, Security Hub, and Inspector pricing before activation.
- [ ] Run Prowler/Checkov/Trivy only after scope, permissions, and cost review.
- [ ] Review IAM, network access, encryption, S3 policy, and public exposure.
- [ ] Save non-sensitive evidence.
- [ ] Delete temporary ALB/WAF and other unused resources.
- [ ] Stop/delete compute and database resources according to data-retention decision.
- [ ] Verify EBS, snapshots, public IPv4, load balancers, NAT, RDS, and other billable resources in all relevant Regions.
- [ ] Recheck billing/credits after usage data updates.
- Acceptance: no unintended lab resources remain; findings and final cost observations recorded.

## Cost and safety gates
- Before every potentially billable action, explain current price assumptions, runtime, storage/network dependencies, ongoing charges, and cleanup.
- Obtain explicit user approval before creating or enabling paid resources.
- Do not assume USD 120 credit covers all services.
- Avoid NAT Gateway and AWS Network Firewall in the base lab unless separately approved.
- Do not commit credentials, private keys, DB passwords, tokens, or sensitive logs.
- AWS infrastructure is Console-first in this iteration.
- No Nginx, DB replication/DBA HA, or claim of host HA from multiple containers on one EC2.
