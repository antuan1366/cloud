# Decision Log

## D-001 — GitHub is the portable project record
Date: 2026-10-25 | Status: Accepted  
Decision: Store state, tasks, architecture, decisions, cost notes, runbooks, and handoff in this repository.  
Reason: Another person or AI must continue without relying on chat history. Update docs after meaningful sessions.

## D-002 — Linux VM for Terraform and Ansible
Date: 2026-10-25 | Status: Accepted in principle; not built  
Decision: Run Terraform and Ansible from a Linux VM under VMware on Windows.  
Reason: Ansible is naturally supported on Linux, and local validation reduces unnecessary cloud usage. Confirm laptop resources first.

## D-003 — Smallest useful initial AWS design
Date: 2026-10-25 | Status: Proposed; deployment approval pending  
Decision: Evaluate one small EC2 host running web and database before separate RDS.  
Reason: Fewer separately billed resources and simpler cleanup. Trade-off: not production-grade or highly available. Cost review required.

## D-004 — Do not assume a plan upgrade extends credits
Date: 2026-10-25 | Status: Accepted  
Decision: Treat access deadline, credit expiry, eligible services, and paid-plan terms as separate facts. Verify in AWS Console before changing plans or provisioning.

## D-005 — Cost warning before billable action
Date: 2026-10-25 | Status: Accepted  
Decision: Explain likely costs, uncertainty, ongoing charges, and cleanup before potentially billable AWS actions. Obtain explicit approval before resource creation.

## D-006 — No secrets or Terraform state in Git
Date: 2026-10-25 | Status: Accepted  
Decision: Ignore state/plans, credentials, keys, and secret-bearing variable files. State and plans may contain sensitive values.
