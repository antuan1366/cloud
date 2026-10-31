# Start Here — Handoff Guide

## Read in this order
1. README.md
2. .ai/STATE.md — authoritative current state.
3. .ai/IMPLEMENTATION_PLAN_6_DAYS.md — current architecture and six-day sequence.
4. .ai/TODO.md — next actions and acceptance criteria.
5. .ai/PROJECT.md
6. Relevant technical docs: ARCHITECTURE, DECISIONS, COST_AND_CLEANUP, SECURITY, RUNBOOK.
7. .ai/SESSION.md — latest handoff and exact next action.
8. .ai/CHANGELOG.md

## Mandatory rules
- Current AWS infrastructure deployment is Console-first. Do not use Terraform or AWS CLI to deploy this iteration.
- The local Ubuntu VM still has Git, Terraform, AWS CLI, and Ansible from earlier learning; those tools are not the deployment path for this scenario.
- Never assume a planned action was completed; verify evidence.
- Give direct, step-by-step instructions and only the steps needed now.
- Before any potentially billable AWS action, explain resource costs, uncertainty, ongoing charges, dependencies, and exact cleanup steps. Obtain explicit user approval before provisioning.
- Recheck AWS credit terms, eligible services, billing visibility, current usage, and existing resources before creating anything.
- Inspect the earlier Terraform-managed EC2 lab before expanding the environment. Do not delete it without explicit approval.
- Prefer least privilege and temporary credentials; do not recommend root access keys for routine work.
- Never ask the user to paste passwords, private keys, MFA codes, payment details, or access keys into chat or Git.
- Do not commit credentials, database passwords, sensitive logs, or personal data.
- Do not claim a test passed without command output or other evidence.
- Distinguish verified facts, user-reported information, plans, and untested assumptions.
- Make the next action explicit and small.
- Only update this repository when the user explicitly asks.

## Current design summary
- One VPC with public, application, database, and management security zones across two AZs.
- One Linux EC2 hosting Docker: two app containers plus one HAProxy or Traefik container.
- No Nginx. Docker container balancing on one host is not EC2-level HA.
- One private Single-AZ Amazon RDS PostgreSQL instance; no DB replication/DBA HA.
- One Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Temporary AWS ALB and WAF exercises; one private S3 bucket.
- No Transit Gateway or dedicated inspection VPC in the base lab.

## Evidence labels
- Verified: directly confirmed by command output, AWS Console, or repository state.
- User-reported: stated by the user, not independently verified.
- Planned: intended but not performed.
- Not tested: no verification evidence yet.
- Blocked: waiting for a specific issue to be resolved.

## Session closeout
Record changes, commands/results, tests, AWS resources (never secrets), dated cost observations, remaining work, and exact next action. Update this repository only when the user explicitly asks.
