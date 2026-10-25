# Architecture

Status: proposed only; deployment is not verified.

## Logical design
Windows laptop
- VMware Workstation
  - Linux automation VM
    - Git
    - Terraform provisions AWS resources
    - Ansible configures the Linux host and services
      - controlled AWS API / SSH access
        - AWS account
          - VPC/network boundary to be finalized
            - one small EC2 instance (initial candidate)
              - web server, e.g. Nginx
              - database, e.g. MariaDB, listening locally/private only

This one-host design is a cost-conscious learning candidate, not highly available or production-grade.

## Network and security
- Never expose the database port to the public internet.
- Allow only required web ports.
- Restrict SSH to a known current public IP where practical; do not open SSH to 0.0.0.0/0.
- Evaluate temporary administration access and Systems Manager only after checking prerequisites, permissions, and costs.
- Use least-privilege roles where possible; avoid long-lived AWS keys on the VM.
- Avoid NAT Gateway for the first version unless explicitly approved after cost review.
- Keep private keys and secrets outside Git.
- Do not put database credentials in Terraform outputs, source control, shell history, or logs.

## Optional separate database
A later version may use EC2 for web and RDS in private subnets. RDS, storage, backups, and networking can incur charges. Do not implement until current pricing and credit eligibility are reviewed with the user.

## Ownership
Terraform manages the AWS infrastructure it creates. Avoid manual changes to managed resources; reconcile any emergency manual change in code/state. Ansible manages OS configuration and services using small, idempotent playbooks.

## Naming and tags
Suggested prefix: scol-lab. Where supported, use tags Project=SecureCloudOperationsLab, Environment=lab, Owner=student. Never put personal secrets in tags.

## Unknowns before implementation
- Exact AWS plan/access terms and credit eligibility.
- Current account inventory and billing.
- AWS region.
- Laptop RAM and VMware status.
- Linux distribution, web server, database, and app/test page.
- Compute size after current cost review.
