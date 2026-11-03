# Changelog

## 2026-11-03 — Core AWS lab and WAF progress recorded
- Recorded deployed VPC, eight workload subnets, IGW, route tables, custom NACLs, and Security Groups.
- Recorded private Amazon Linux EC2 with Docker/Nginx, SSM Session Manager access, and least-privilege S3 image retrieval.
- Recorded internet-facing ALB, healthy target on port 8080, HTTPS listener, and HTTP-to-HTTPS redirect.
- Documented self-signed TLS certificate limitation; browser trust warning is expected and certificate is not production-trusted.
- Recorded private Single-AZ PostgreSQL RDS and verified EC2-to-RDS connectivity.
- Recorded private S3 bucket, encryption, IAM read-only exercise, S3 Gateway Endpoint, and denied anonymous/upload access tests.
- Recorded App-A VPC Flow Logs in CloudWatch and observed REJECT traffic.
- Recorded WAF association/logging and successful SQL injection block test.
- Recorded Network Firewall access issue. User created firewall-subnet-a (10.10.41.0/24), but no policy or firewall was created; task is postponed.
- Updated current state, backlog, and session handoff to distinguish deployed resources from planned work.

## 2026-10-31 — Six-day Console-first lab redesign
- Replaced the initial one-host web/database concept with a proposed one-VPC architecture using public, application, database, and management security zones across two AZs.
- Switched infrastructure deployment for this iteration to the AWS Management Console; Terraform/AWS CLI are not used for deployment.
- Planned a Linux EC2 with Docker and internal application load balancing; actual deployed learning exercise later used Nginx.
- Clarified that container load balancing on one EC2 is not host-level or AZ-level HA.
- Planned one private Single-AZ Amazon RDS PostgreSQL instance and one Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Added temporary ALB/WAF exercises and private S3 storage.
- Added cost gates and cleanup guidance in .ai/IMPLEMENTATION_PLAN_6_DAYS.md.

## 2026-10-27 — Local tooling prepared
- Installed and verified Terraform v1.17.0, AWS CLI v2.38.6, Git 2.43.0, and Ansible core 2.21.5 in the user's Ubuntu VM.
- These tools remain available for learning; current AWS infrastructure was configured through the Console.

## 2026-10-25 — Initial documentation
- Defined project purpose and learning outcomes.
- Recorded user-reported environment and AWS credit/access deadline.
- Added cost-first provisioning and cleanup rules.
- Added security requirements and Git protections for secrets and Terraform state.
