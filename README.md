# Secure Cloud Operations Lab

A practical, cost-conscious lab for deploying and securing a small AWS web service and database, managed with Terraform and Ansible from a Linux VM under VMware on Windows.

## Current status
- Phase: 0 — local tooling prepared; AWS account review and authentication not yet completed.
- AWS Console access: user-reported.
- AWS credit: USD 120 remaining, as previously reported by the user; recheck live balance and terms.
- Access/free-plan message: previously reported as ending on 5 November 2026 or when credits are depleted. Recheck current terms.
- Ubuntu VM: Ubuntu 24.04.5 LTS, user-reported/previously checked.
- Git: 2.43.0, verified.
- Terraform: v1.17.0, verified.
- Ansible: core 2.21.5 in `~/ansible-venv`, verified.
- AWS CLI: v2.38.6, verified.
- No AWS CLI credentials/profile configured or verified.
- No project AWS resources have been created.

Start with .ai/START_HERE.md and .ai/STATE.md.

## Intended result
Use Git for version control, Terraform to provision minimum AWS infrastructure, and Ansible to configure a Linux host running a web server and database. Apply network restrictions, test behavior, document costs, and verify cleanup.

## Proposed approach
1. Verify AWS account access type, terms, credits, billing, MFA, and existing resources.
2. Use the local Ubuntu VM for Git, Terraform, Ansible, and AWS CLI.
3. Validate Terraform locally before provisioning.
4. Review current prices and credit eligibility before creating any AWS resource.
5. Initially evaluate one small EC2 instance hosting both web and database services. This is a learning setup, not production architecture.
6. Consider a separate RDS database only after a separate cost review.
7. Test security and functionality, then remove lab resources and verify cleanup.

## Cost and security rules
- No potentially billable AWS action before a clear warning and explicit user approval.
- Budgets/alerts are notifications, not guaranteed spending caps.
- Stopping EC2 does not necessarily stop charges for storage, snapshots, public IPv4, or other resources.
- Avoid NAT Gateway, load balancers, and always-on managed databases initially unless approved after cost review.
- Never commit credentials, private keys, Terraform state, secret-bearing variable files, or sensitive plans.
- Distinguish verified facts from user-reported information, plans, and untested assumptions.

## Documents
- .ai/START_HERE.md — handoff instructions.
- .ai/PROJECT.md — scope and learning goals.
- .ai/STATE.md — authoritative current state.
- .ai/TODO.md — prioritized tasks and acceptance criteria.
- .ai/ARCHITECTURE.md — proposed architecture.
- .ai/DECISIONS.md — decisions and rationale.
- .ai/COST_AND_CLEANUP.md — cost risks and teardown.
- .ai/SECURITY.md — security and secrets policy.
- .ai/RUNBOOK.md — commands and operational procedures.
- .ai/SESSION.md — latest session handoff.
- .ai/CHANGELOG.md — meaningful changes.

After each meaningful session, update STATE, TODO, and SESSION, plus other documents affected by changes. Only update this repository when the user explicitly asks.
