# Latest Session Handoff

Date: 2026-10-25  
Session: initial project documentation  
Status: documentation initialized; implementation not started.

## Goal
Build an AWS web server and database, managed by Terraform and configured by Ansible from a VMware Linux VM on Windows. Minimize credit consumption and make the repository sufficiently precise for another person or AI to continue.

## Environment
- Windows laptop: user-reported.
- AWS Console access: user-reported.
- Credit: USD 120 shown in console, user-reported.
- Access/free-plan message: ends 2026-11-05 or when credits are depleted, user-reported.
- User earlier saw 13 days remaining; recheck because relative time changes.
- Git and Terraform not installed: user-reported.
- VMware/Linux VM and Ansible status: not confirmed.
- No project AWS resources confirmed.

## Repository
- URL: https://github.com/antuan1366/cloud
- Default branch: main.
- Visibility: public.
- GitHub integration reported admin/push permission.

## Decisions
- Terraform and Ansible run from Linux VM under VMware.
- First cloud candidate is a minimum-resource design, possibly one EC2 host for web + DB.
- RDS is optional later after cost review.
- No AWS resource creation before a cost warning and explicit approval.
- Never assume a plan upgrade extends credits or makes all services free.

## Completed
- [x] Initial docs created (verify individual files in GitHub).
- [ ] No tools installed.
- [ ] No AWS resources provisioned.

## Exact next action
1. Check current AWS Credits, eligible services, expiry, Bills/usage, and plan terms.
2. Check whether budgets/alerts exist and MFA is enabled.
3. Review existing AWS resources.
4. Confirm VMware Workstation status and laptop RAM.
5. Install Git on Windows and verify git --version.
6. Clone the repository and prepare Linux VM.
7. Do not provision AWS until costs/terms are reviewed.

## Notes for next assistant
Give only instructions needed for the current step. Before any potentially billable AWS action, explain costs and cleanup and request approval. Update this handoff at the end of the next session.
