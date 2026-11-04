# Latest Session Handoff

Date: 2026-11-04  
Session: Added cloud infrastructure auditing to the learning roadmap  
Status: Documentation updated; the new audit curriculum is planned and has not yet been performed.

## User's current goal
Build practical Cloud Security Engineering capability through a cost-controlled AWS lab and structured learning. The user decided not to apply for the Upwork DevSecOps/SOC 2 readiness job discussed on 2026-11-04. This is a decision about that specific job, not a rejection of learning cloud auditing.

## New learning decision
- Add cloud infrastructure auditing to the learning plan.
- Focus on technical AWS security assessment, control reviews, evidence collection, findings, remediation, retesting, and reporting.
- Include framework familiarity with CIS AWS Foundations Benchmark, AWS Well-Architected, NIST, ISO/IEC 27001, and relevant SOC 2 Trust Services Criteria.
- Keep formal SOC 2 attestation outside the user's role: a qualified independent CPA firm performs the formal examination and issues the report.
- Do not claim CPA status, independent SOC 2 auditor status, authority to certify, or experience the user does not have.
- The new curriculum is documented in .ai/CLOUD_AUDIT_LEARNING_PLAN.md.
- The user explicitly requested this GitHub update.

## Existing AWS lab direction
- One VPC with public, application, database, and management security zones.
- Two Availability Zones for subnet and managed-service learning.
- Remove Nginx.
- One Linux EC2 (provisional t3.medium) running Docker.
- Two application containers plus one HAProxy or Traefik container for internal load balancing.
- Container balancing on one EC2 is not host-level or AZ-level HA.
- One private Amazon RDS PostgreSQL instance, Single-AZ initially.
- Database replication and DBA-focused HA are out of scope.
- One Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Temporary AWS Application Load Balancer and AWS WAF exercises.
- One private S3 bucket for object-storage/backup/log learning.
- No Transit Gateway or dedicated inspection VPC in the base architecture.
- AWS infrastructure deployment is Console-first; no Terraform or AWS CLI deployment in this iteration.
- Potentially billable actions require a cost explanation and explicit user approval.

## Account context — user-reported, not freshly verified
- Previously reported AWS credit balance: USD 120.
- Previously reported access/free-plan end date: 2026-11-05 or when credits are depleted.
- Recheck balance, terms, service eligibility, usage, and Region before deployment.

## Repository changes in this session
- Added .ai/CLOUD_AUDIT_LEARNING_PLAN.md.
- Updated README.md, .ai/PROJECT.md, and .ai/TODO.md to include the new audit track.
- Updated .ai/CHANGELOG.md.
- No AWS resources were created or changed.

## Suggested next step
When the user is ready, resume the existing AWS lab in its current order and later work through the cloud audit curriculum as a separate learning phase. Start with scope/authorization and asset inventory, then assess the lab controls. Do not jump into paid AWS services without checking pricing and obtaining approval.

## Notes for next assistant
- Be direct, interactive, and step-by-step.
- The user chose not to apply for the SOC 2 readiness job; do not draft a proposal for it.
- The user does want cloud auditing included in their learning roadmap.
- Do not equate ISO 27001 familiarity with SOC 2 delivery experience.
- Do not claim the new audit curriculum is completed; it is only documented.
- Only update GitHub again if the user explicitly asks.
