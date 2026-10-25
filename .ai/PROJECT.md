# Project Definition

## Purpose
Build a small AWS web service and database, provision infrastructure with Terraform, configure Linux services with Ansible, and apply practical cloud operations and security controls while minimizing credit consumption.

## Environment
- Windows laptop: user-reported.
- AWS Console access: user-reported.
- AWS credit: USD 120 displayed, user-reported.
- AWS access/free-plan deadline: 5 November 2026, user-reported; verify live terms.
- Git and Terraform not installed: user-reported.
- VMware and Linux VM status: not confirmed.
- Ansible will run from the Linux control VM; installation not confirmed.

## User goal
Create a web server and database on AWS, while running Terraform and Ansible on a VMware Linux VM on the laptop. The user may consider changing to a paid plan near the end of the access period; first verify exact terms. Never assume an upgrade extends credits or makes all services free.

## Learning outcomes
1. Track infrastructure and docs with Git.
2. Learn IAM, VPC, EC2, security groups, and AWS billing.
3. Write and validate Terraform.
4. Use Ansible inventory, playbooks, variables, handlers, and idempotent tasks.
5. Administer Linux web and database services.
6. Restrict database exposure and management access.
7. Test connectivity and troubleshoot systematically.
8. Understand logs, updates, backups, recovery, and cleanup.
9. Produce a reproducible handoff.

## First-version scope
- A small web service.
- A database used by that service.
- Terraform-managed AWS infrastructure.
- Ansible-managed host configuration.
- Security controls, tests, and teardown documentation.

## Proposed staging
First evaluate one small EC2 host running both web and database services. This may reduce separate service charges, but is a learning architecture and not production-grade. Consider RDS only after checking current pricing, credit eligibility, and learning value.

## Out of scope initially
High availability, multi-region, Kubernetes, complex CI/CD, production data, and expensive networking/database resources without explicit cost review.

## Definition of done
- Infrastructure is version-controlled in Terraform.
- Ansible configuration is repeatable.
- Web response and database connectivity are tested.
- Database is not unnecessarily public.
- Test commands and outcomes are documented.
- Teardown is performed and remaining billable resources are checked.
- Docs distinguish verified outcomes from assumptions.
