# Secure Cloud Operations Lab

A practical, cost-conscious lab for deploying and securing a small AWS web service and database, managed with Terraform and Ansible from a Linux VM under VMware on Windows.

## Current status
- Phase: 0 — preparation; no project AWS resources confirmed.
- AWS Console access: user-reported.
- Credit: USD 120 remaining, as shown by the user in AWS Console.
- Access/free-plan message: ends on 5 November 2026 or when credits are depleted, as reported by the user. Recheck live terms; the previously displayed “13 days” is time-sensitive.
- Windows laptop: user-reported.
- Git and Terraform: not installed, user-reported.
- VMware/Linux VM and Ansible status: not yet confirmed.

Start with .ai/START_HERE.md and .ai/STATE.md.

## Intended result
Use Git for version control, Terraform to provision minimum AWS infrastructure, and Ansible to configure a Linux host running a web server and database. Apply network restrictions, test behavior, document costs, and verify cleanup.

## Proposed approach
1. Verify account terms, credits, billing, MFA, and existing resources.
2. Prepare Git on Windows and a Linux VM under VMware.
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

After each meaningful session, update STATE, TODO, and SESSION, plus other documents affected by changes.
