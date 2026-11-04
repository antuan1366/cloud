# Changelog

## 2026-11-04 — Added cloud infrastructure auditing curriculum
- Added .ai/CLOUD_AUDIT_LEARNING_PLAN.md with a structured AWS technical audit curriculum.
- Covered assessment scope and authorization, asset discovery, IAM, network security, data protection, logging, vulnerability management, configuration, backup/recovery, incident response, and resilience.
- Added framework mapping guidance for CIS AWS Foundations Benchmark, AWS Well-Architected, NIST, ISO/IEC 27001, and relevant SOC 2 Trust Services Criteria.
- Added evidence handling, risk-rated findings, remediation, retesting, and technical reporting exercises.
- Clarified that the curriculum does not authorize the learner to issue SOC 2 reports or act as an independent CPA auditor.
- Updated README, PROJECT, TODO, and SESSION documentation.
- User decided not to apply for the discussed SOC 2/DevSecOps Upwork job.
- No AWS resources were created or changed.

## 2026-10-31 — Six-day Console-first lab redesign
- Replaced the initial one-host web/database concept with a proposed one-VPC architecture using public, application, database, and management security zones across two AZs.
- Switched infrastructure deployment for this iteration to the AWS Management Console; Terraform/AWS CLI are not used for deployment.
- Removed Nginx.
- Planned one Linux EC2 with Docker: two application containers and one HAProxy or Traefik container.
- Clarified that container load balancing on one EC2 is not host-level or AZ-level HA.
- Added one private Single-AZ Amazon RDS PostgreSQL instance; database replication/DBA HA excluded.
- Added one Windows Server EC2 for Microsoft RDS learning, with licensing and secure-access caveats.
- Added temporary AWS ALB and AWS WAF exercises, plus a private S3 bucket.
- Kept EFS optional; excluded Transit Gateway and dedicated inspection VPC from the base lab.
- Added detailed six-day sequence, acceptance criteria, cost gates, and cleanup guidance in .ai/IMPLEMENTATION_PLAN_6_DAYS.md.
- No new AWS resources were created by this documentation update.

## 2026-10-27 — Local tooling prepared
- Installed and verified Terraform v1.17.0 on Ubuntu 24.04.5 LTS.
- Installed and verified AWS CLI v2.38.6.
- Verified Git 2.43.0.
- Verified Ansible core 2.21.5 in the user's ~/ansible-venv; localhost ping had previously succeeded.
- Confirmed day-to-day shell is the normal antuan account, not root.
- Earlier lab AWS CLI authentication and Terraform deployment were completed later; see .ai/STATE.md for historical verified results.
- No resources for the revised six-day architecture have been created.

## 2026-10-25 — Initial documentation
- Defined project purpose and learning outcomes.
- Recorded user-reported environment and AWS credit/access deadline.
- Documented proposed local Linux automation VM and minimal AWS web/database design.
- Added cost-first provisioning and cleanup rules.
- Added security requirements and Git protections for secrets and Terraform state.
- Added handoff guide and prioritized backlog.
- No AWS resources were created during documentation initialization.

## 2026-11-04 — Added EC2 security and monitoring practice track
- Added .ai/EC2_SECURITY_MONITORING_PRACTICE_PLAN.md for EC2 hardening, disk monitoring, dashboards, email alerts, and scheduled storage reports.
- Documented practice gaps in CloudWatch Agent, guest memory/filesystem metrics, IAM instance roles, dashboards, alarms, SNS, and scheduled reporting.
- Added prerequisites, staged exercises, acceptance criteria, evidence requirements, and cost gates.
- Clarified that standard CPU/network metrics differ from guest RAM/disk metrics, and alarms differ from periodic reports.
- No AWS resources were created or changed.
