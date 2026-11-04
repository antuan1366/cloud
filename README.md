# Secure Cloud Operations Lab

A cost-controlled, console-first AWS security learning lab. The current plan covers VPC segmentation, Dockerized web application deployment, Amazon RDS PostgreSQL, Microsoft Remote Desktop Services, AWS Application Load Balancer, AWS WAF, storage, monitoring, and security assessment.

## Current project direction
- AWS infrastructure for the new scenario will be configured through the AWS Management Console.
- Terraform and AWS CLI will not be used to deploy this iteration.
- Linux application tier: one EC2 host running Docker, with two application containers and one HAProxy or Traefik load-balancer container.
- No Nginx.
- Database tier: one private Amazon RDS PostgreSQL instance, initially Single-AZ. Database replication/DBA HA is out of scope.
- Management tier: one Windows Server EC2 for Microsoft Remote Desktop Services learning. This is not a production RDS farm.
- Network: one VPC, multiple logical security zones, and two Availability Zones.
- Temporary learning exercises: AWS ALB, AWS WAF, S3, CloudTrail, CloudWatch, and selected security assessment tools.
- Docker container load balancing is not EC2-level high availability.

## Additional learning track: Cloud Infrastructure Auditing
The lab now includes a dedicated cloud-auditing learning track covering authorized AWS scope definition, asset and architecture discovery, IAM/network/data/logging/vulnerability/backup reviews, framework mapping, evidence collection, findings, remediation, retesting, and technical reporting.

See [.ai/CLOUD_AUDIT_LEARNING_PLAN.md](.ai/CLOUD_AUDIT_LEARNING_PLAN.md).

This is technical assessment and audit-readiness training. It does not authorize the learner to issue a SOC 2 report or act as an independent CPA auditor.

## Account and cost context
- AWS credits: USD 120 remaining was previously reported by the user; recheck live balance and eligible services.
- Access/free-plan deadline: 5 November 2026 was previously reported; recheck live terms.
- The user requires a cost warning and explicit approval before any potentially billable AWS action.
- Stopping EC2 does not stop EBS storage charges or all networking charges. ALB, WAF, NAT Gateway, and Network Firewall may charge independently.
- Do not assume promotional credits cover every service.
- The previous learning exercise deployed a Terraform-managed EC2 web server. Its current running state and all related resources must be inspected in the AWS Console before adding new resources.

## Six-day plan
See [.ai/IMPLEMENTATION_PLAN_6_DAYS.md](.ai/IMPLEMENTATION_PLAN_6_DAYS.md) for architecture, subnet zones, day-by-day tasks, acceptance criteria, cost guardrails, and cleanup.

## Documentation
- .ai/START_HERE.md — handoff instructions.
- .ai/STATE.md — authoritative current state.
- .ai/PROJECT.md — scope and learning goals.
- .ai/TODO.md — prioritized tasks and acceptance criteria.
- .ai/ARCHITECTURE.md — current proposed architecture.
- .ai/DECISIONS.md — decisions and rationale.
- .ai/COST_AND_CLEANUP.md — cost risks and teardown.
- .ai/SECURITY.md — security and secrets policy.
- .ai/RUNBOOK.md — operational procedures.
- .ai/SESSION.md — latest session handoff.
- .ai/CHANGELOG.md — meaningful changes.
- .ai/CLOUD_AUDIT_LEARNING_PLAN.md — cloud infrastructure auditing curriculum.

## Rules
- Never create a potentially billable AWS resource without explaining costs, ongoing charges, and cleanup, then receiving explicit approval.
- Verify account credits, eligible services, billing, and existing resources before deployment.
- Treat all commits as public; never commit secrets, private keys, credentials, sensitive logs, or personal data.
- Distinguish verified facts, user-reported information, plans, and untested assumptions.
- Only update this repository when the user explicitly asks.

## Additional learning track: EC2 Security and Monitoring
A job-aligned practice track has been added for EC2 hardening, least-privilege IAM instance roles, CloudWatch Agent memory/filesystem metrics, dashboards, 80%/90% disk alarms, SNS email notifications, and scheduled per-filesystem storage reports.

See [.ai/EC2_SECURITY_MONITORING_PRACTICE_PLAN.md](.ai/EC2_SECURITY_MONITORING_PRACTICE_PLAN.md). This is planned practice only; no AWS resources have been deployed for it. The plan distinguishes standard EC2 CPU/network metrics from guest-level RAM/disk metrics, and threshold alerts from periodic capacity reports.

The practice may incur charges for EC2, EBS, CloudWatch metrics/alarms/dashboards/logs, SNS, Lambda, and EventBridge. Cost review and explicit approval are required before enabling or creating resources.
