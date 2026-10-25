# Current State

Last updated: 2026-10-25  
Status: Phase 0 — preparation. No project AWS resources confirmed.

## Facts and status
- User-reported: AWS Console is accessible.
- User-reported: AWS Credits page showed USD 120.00 remaining.
- User-reported: Console said free access ends on 5 November 2026 or when credits are depleted. The user initially saw 13 days remaining. Recheck the live console because the remaining-days count changes.
- User-reported: Windows laptop.
- User-reported: Git and Terraform are not installed.
- User-reported: Wants Terraform and Ansible in a VMware Linux VM.
- User-reported: Wants a web server and database on AWS.
- Verified via GitHub integration: repository antuan1366/cloud exists, default branch main, public visibility, connected integration reports admin/push permission.
- Not yet verified: VMware installation, Linux VM, laptop RAM, AWS account/plan terms, credit eligibility/expiry details, current bill, budgets, MFA, existing resources, and resource costs.
- Not done based on available evidence: tool installation or AWS provisioning for this lab.

## Proposed architecture
See ARCHITECTURE.md. Candidate: one small EC2 instance for web and database, with database access restricted to localhost/private access. This is not production architecture and requires a cost review before deployment.

## Cost posture
- Reported credit balance: USD 120.
- Reported deadline: 2026-11-05.
- Exact current balance, remaining time, billing usage, credit eligibility, and post-deadline behavior must be rechecked.
- Do not assume plan upgrade extends credits or makes all services free.
- No resource creation before a cost warning and explicit user approval.

## Immediate next action
1. Re-open AWS Billing and Cost Management.
2. Check Credits: current balance, expiry, eligible services, and terms.
3. Check Bills/current usage.
4. Check whether a budget and billing alert exist.
5. Check MFA/security status without sharing codes or secrets.
6. Review existing AWS resources in relevant regions.
7. Confirm VMware Workstation status and laptop RAM.

Then prepare local tools and a Linux VM. Do not provision AWS until terms and cost have been reviewed.

## Update policy
Replace stale values when newer evidence arrives. Date all balances, deadlines, inventory checks, and test results.
