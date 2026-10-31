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

## Rules
- Never create a potentially billable AWS resource without explaining costs, ongoing charges, and cleanup, then receiving explicit approval.
- Verify account credits, eligible services, billing, and existing resources before deployment.
- Treat all commits as public; never commit secrets, private keys, credentials, sensitive logs, or personal data.
- Distinguish verified facts, user-reported information, plans, and untested assumptions.
- Only update this repository when the user explicitly asks.
