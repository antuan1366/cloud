# Task Backlog

Status: [ ] not started, [~] in progress, [x] verified complete, [!] blocked. Mark complete only when acceptance criteria are met.

## P0 — Account safety
- [ ] Recheck AWS credit balance, expiry, eligible services, and plan terms. Acceptance: dated evidence recorded.
- [ ] Inspect Bills/current usage. Acceptance: current usage status recorded; do not infer future cost from a zero bill.
- [ ] Check budget/alerts. Acceptance: status recorded; warn before creating anything that could cost money.
- [ ] Check root/privileged MFA status without sharing codes.
- [ ] Inventory existing resources in relevant AWS regions before provisioning.
- [ ] Confirm VMware status and laptop RAM.

## P1 — Local environment
- [ ] Install Git for Windows. Acceptance: git --version works in PowerShell.
- [ ] Clone this repository and verify git status.
- [ ] Install/prepare VMware and a Linux VM if needed.
- [ ] Install Terraform in Linux VM from official HashiCorp instructions. Acceptance: terraform version works.
- [ ] Install Ansible in Linux VM using supported distribution instructions. Acceptance: ansible --version works.
- [ ] Configure Git identity/access safely; never commit private keys.

## P2 — Design and local validation
- [ ] Choose Linux distribution, web server, database, and test page.
- [ ] Design minimum AWS resource set and review costs.
- [ ] Add Terraform configuration, provider/version constraints, variables example, and outputs.
- [ ] Run terraform fmt -check and terraform validate locally.
- [ ] Review Terraform plan for unexpected resources.
- [ ] Explain costs/cleanup and obtain explicit approval before first apply.

## P3 — Minimal deployment
- [ ] Create only approved resources.
- [ ] Restrict management access to the user's current public IP where practical.
- [ ] Keep database port private.
- [ ] Use Ansible to configure services.
- [ ] Test web response, database connectivity, and denied unauthorized access.
- [ ] Record safe resource identifiers, region, tests, results, and cleanup.

## P4 — Operations and teardown
- [ ] Review security-group rules, OS updates, service permissions, database auth, and logs.
- [ ] Document backups/recovery and run a safe recovery exercise if feasible.
- [ ] Review and approve terraform destroy before execution.
- [ ] Verify EC2, volumes, snapshots, public IP resources, NAT Gateway, load balancers, RDS, and other created resources are removed.
- [ ] Recheck billing/credits after billing data updates.

## P5 — Optional advanced work (cost review required)
- [ ] Compare single-host DB with RDS.
- [ ] Add RDS only after explicit cost approval.
- [ ] Add CI validation for Terraform/Ansible.
- [ ] Add logging/security services only when justified and cost-reviewed.
