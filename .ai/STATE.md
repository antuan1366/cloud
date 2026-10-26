# Current State

Last updated: 2026-10-27  
Status: Phase 0 — local tooling prepared; AWS account review and authentication not yet completed.

## Facts and status

### Local environment — verified by command output
- Windows laptop running VMware with an Ubuntu VM.
- Ubuntu VM upgraded to Ubuntu 24.04.5 LTS (user-reported and previously verified with `lsb_release -a`).
- Normal Linux user: `antuan`; hostname shown as `juniper`.
- Git 2.43.0 installed and working.
- Terraform v1.17.0 installed and working (`terraform version`).
- AWS CLI v2.38.6 installed and working (`aws --version`).
- Python 3.12.3 available in Ubuntu.
- Ansible core 2.21.5 installed in `/home/antuan/ansible-venv`; the venv was activated during verification.
- `ansible localhost -m ping` succeeded earlier from the virtual environment.
- A system-wide Ansible 2.16.3 also exists at `/usr/bin/ansible`; prefer the virtual environment for this project.
- Git, Terraform, Ansible, and AWS CLI were verified from the normal `antuan` account. AWS CLI and Terraform were installed system-wide using sudo/root, but are available to `antuan`.

### AWS account — user-reported, must be rechecked
- AWS Console is accessible.
- AWS Credits page previously showed USD 120.00 remaining.
- Console message previously said free access ends on 5 November 2026 or when credits are depleted.
- Current credit balance, expiry terms, eligible services, billing/usage, budgets/alerts, MFA, account access type, region, and existing resources have not been verified in this session.

### Not yet done
- AWS CLI credentials/profile have not been configured.
- No AWS identity has been verified with `aws sts get-caller-identity`.
- No project AWS resources have been created by this lab.
- No Terraform configuration has been applied.
- AWS CLI agent toolkit/MCP setup has not been used.
- Terraform has not yet been tested against AWS.
- Repository has not been confirmed cloned to the Ubuntu VM.

## Proposed architecture
See ARCHITECTURE.md. Candidate: one small EC2 instance for web and database, with database access restricted to localhost/private access. This is a learning design, not production architecture, and requires cost review before deployment.

## Cost posture
- Reported credit balance: USD 120; last reported before this update, not freshly verified.
- Reported deadline: 2026-11-05; recheck live account terms.
- No AWS resource creation before a clear cost warning and explicit user approval.
- Do not assume a plan upgrade extends credits or makes all services free.
- Budget alerts are notifications, not guaranteed spending caps.

## Immediate next action
1. Before configuring AWS access, ask how the user signs in (root, IAM user, IAM Identity Center/SSO, or credentials provided by another person).
2. Prefer a supported secure authentication method; do not ask the user to paste secrets into chat.
3. Recheck current credits/expiry/eligible services, current usage, budgets/alerts, MFA, region, and existing AWS resources.
4. Only then plan the minimum-resource deployment and explain expected charges and cleanup.
5. Do not run `terraform apply` or create AWS resources without explicit approval.

## Update policy
Only update this repository when the user explicitly asks. Replace stale values when newer evidence arrives. Date balances, deadlines, inventory checks, and test results.
