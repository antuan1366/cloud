# Secure Cloud Operations Lab

A cost-controlled AWS cloud infrastructure and security learning lab. The deployed exercises cover VPC segmentation, private Linux compute, Docker, Amazon RDS PostgreSQL, ALB/HTTPS, AWS WAF, private S3, IAM, Systems Manager, and CloudWatch monitoring.

## Current status (2026-11-03)
- Core AWS network and workload foundation deployed in us-east-1.
- VPC: secure-cloud-lab-vpc (10.10.0.0/16), with eight workload subnets across two AZs.
- Private Amazon Linux EC2 running Docker and an Nginx container; administration through Systems Manager Session Manager without SSH.
- Internet-facing ALB with healthy EC2 target, HTTPS listener, and HTTP-to-HTTPS redirect.
- ACM certificate is self-signed and not publicly trusted; this is a learning setup, not production TLS.
- Private Single-AZ PostgreSQL RDS; EC2-to-RDS connectivity verified.
- Private S3 bucket, encryption, read-only IAM exercise, and S3 Gateway Endpoint.
- App-A VPC Flow Logs delivered to CloudWatch Logs.
- AWS WAF attached to ALB; SQL injection test was blocked and logged.
- Network Firewall postponed: firewall-subnet-a was created, but Network Firewall console pages returned an account/service-access error. No firewall policy or firewall exists.

## Next learning areas
- Cost/billing review and complete security validation/cleanup.
- Dedicated application DB identity and recovery testing.
- Windows Server / Microsoft Remote Desktop Services.
- VPN exercise.
- Terraform representation of the existing environment, followed by safe Ansible automation and CI checks.
- Optional centralized SOC log analytics with OpenSearch after a separate cost review.

## Documentation
- .ai/START_HERE.md — handoff instructions.
- .ai/STATE.md — authoritative deployed state and next actions.
- .ai/PROJECT.md — scope and learning goals.
- .ai/TODO.md — prioritized backlog and acceptance criteria.
- .ai/ARCHITECTURE.md — architecture reference (review alongside current state).
- .ai/DECISIONS.md — decisions and rationale.
- .ai/COST_AND_CLEANUP.md — cost risks and teardown.
- .ai/SECURITY.md — security and secrets policy.
- .ai/RUNBOOK.md — operational procedures.
- .ai/SESSION.md — latest handoff.
- .ai/CHANGELOG.md — meaningful changes.

## Rules
- Before any new potentially billable AWS action, explain costs, ongoing charges, dependencies, and cleanup; obtain explicit approval.
- Recheck AWS credits, eligible services, billing visibility, and existing resources; previously reported balance/deadline are not current verification.
- Treat all commits as public; never commit secrets, private keys, credentials, sensitive logs, or personal data.
- Distinguish verified facts, user-reported information, plans, and untested assumptions.
- Only update this repository when the user explicitly asks.
