# Latest Session Handoff

Date: 2026-10-27  
Session: local automation tool setup  
Status: local tools installed and verified; AWS access and provisioning not started.

## Goal
Build a cost-conscious AWS web server and database lab managed with Terraform and Ansible from a VMware Ubuntu VM on Windows. Preserve AWS credits and document safe cleanup.

## Environment and verified results
- Ubuntu VM hostname shown as `juniper`; normal user is `antuan`.
- Ubuntu version reported/previously checked: 24.04.5 LTS.
- Git: 2.43.0.
- Terraform: v1.17.0 on linux_amd64.
- AWS CLI: v2.38.6.
- Python: 3.12.3.
- Ansible venv: `~/ansible-venv`, Ansible core 2.21.5.
- System Ansible also exists as core 2.16.3 at `/usr/bin/ansible`; use the venv by running `source ~/ansible-venv/bin/activate`.
- Ansible localhost ping previously succeeded.
- AWS CLI and Terraform are installed system-wide and are available to `antuan`.
- GitHub repo: https://github.com/antuan1366/cloud; default branch main; public.
- No AWS CLI credentials/profile have been configured or verified.
- No project AWS resources have been created.

## User-reported account context (not freshly verified)
- AWS Credits page previously showed USD 120 remaining.
- Console message previously said free access ends on 2026-11-05 or when credits are depleted.
- Recheck live terms, current balance, eligible services, and current usage before deployment.

## Decisions
- Terraform provisions infrastructure; Ansible configures OS/services; Git versions project files; AWS CLI is for AWS API/terminal access.
- Run normal development as `antuan`, not root. Use `sudo` only when needed.
- Keep Ansible activated in `~/ansible-venv` when using project Ansible commands.
- Candidate first architecture: one small EC2 instance with web and database on the same host, database private/localhost only. Not production-grade.
- RDS, NAT Gateway, load balancers, and other extra resources require separate cost review.
- No AWS resource creation before a cost warning and explicit approval.
- Never ask the user to paste access keys, secret keys, session tokens, MFA codes, or passwords into chat.
- The user explicitly instructed that GitHub docs should only be updated when they ask. This update was made in response to their explicit request.

## Completed in this session
- [x] Installed Terraform v1.17.0 and verified `terraform version`.
- [x] Installed AWS CLI v2.38.6 and verified `aws --version`.
- [x] Verified Git 2.43.0.
- [x] Switched from root to `antuan` and verified Ansible core 2.21.5 in its venv.
- [x] Earlier local test: `ansible localhost -m ping` returned SUCCESS.
- [x] Updated this handoff and project status documents on GitHub after explicit user request.

## Exact next action
Ask how the user signs into AWS Console (root, IAM user, IAM Identity Center/SSO, or credentials provided by another person). Based on that answer, choose a secure CLI authentication method. Do not configure credentials before clarifying access type and do not request secrets in chat.

After authentication is established, verify identity with `aws sts get-caller-identity`, then review credits, terms, usage, budget alerts, MFA, region, and existing resources. Do not apply Terraform until costs and cleanup have been explained and the user explicitly approves.

## Notes for next assistant
Give one manageable step at a time. Avoid broad command dumps. Clearly distinguish completed work from proposed work and user-reported facts. Do not update GitHub again unless explicitly asked.
