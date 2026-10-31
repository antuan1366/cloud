# Project Definition

## Purpose
Build a small, cost-controlled AWS environment to learn cloud infrastructure and security through the AWS Management Console. Focus: network segmentation, Docker, managed databases, Windows remote administration, load balancing, WAF, storage, monitoring, and security assessment.

## User goal
Develop practical Cloud Security Engineering capability by building, securing, testing, and documenting a realistic small AWS environment. Relevant background includes network/infrastructure administration, vulnerability management, security auditing, firewalls/WAF, Splunk, Windows/Linux, and networking.

## Current scope
- Console-first AWS infrastructure configuration; no Terraform or AWS CLI deployment in this iteration.
- One VPC with public, application, database, and management security zones.
- Two Availability Zones for subnet and managed-service learning.
- One Linux EC2 t3.medium (provisional) running Docker.
- Two application containers and one HAProxy or Traefik container on the same EC2 host.
- No Nginx.
- One private Amazon RDS PostgreSQL instance, initially Single-AZ.
- No database replication or DBA-focused HA.
- One Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Temporary AWS Application Load Balancer and AWS WAF exercises.
- One private S3 bucket for object storage/backup/log learning.
- Security Groups, NACLs, IAM, CloudTrail, CloudWatch, and selected security assessment tools.

## Architecture principles
- Security zones are logical trust areas; Availability Zones are separate AWS infrastructure locations.
- Use private subnets for application, database, and management workloads where practical.
- Do not expose RDS publicly or RDP to the entire internet.
- Use least-privilege Security Groups and IAM permissions.
- Docker container load balancing on one EC2 does not provide host-level or AZ-level HA.
- ALB is a separate managed AWS service with independent charges.
- EFS is optional and not required for the proposed stateless app.
- Transit Gateway and centralized inspection VPC are advanced follow-up topics, not part of the base lab.

## Six-day outcomes
1. Build VPC, subnets, route tables, Security Groups, and NACLs in the Console.
2. Deploy Linux EC2 and Docker app containers with internal load balancing.
3. Deploy private RDS PostgreSQL and test access controls; learn S3 object security.
4. Deploy Windows Server and learn Microsoft RDS roles and secure administration.
5. Configure/test AWS ALB and AWS WAF; compare third-party WAF/firewall products.
6. Review CloudTrail, CloudWatch, posture, selected vulnerability tools, and cleanup.

## Exclusions
- Nginx.
- Database replication/failover and DBA HA.
- Production HA claims from one EC2 host or one Windows server.
- Production multi-server Microsoft RDS farm.
- Transit Gateway/inspection VPC in the base design.
- Paid firewall appliance deployment without separate licensing and cost approval.
- Terraform/AWS CLI infrastructure deployment in this iteration.

## Definition of done
- Network architecture and access matrix documented.
- Application responds through Docker proxy; container failure behavior tested.
- Application connects to private RDS using a least-privilege account.
- S3 is private and encryption/access/versioning behavior tested.
- Windows remote administration path is secured and Microsoft RDS roles understood.
- ALB health checks and WAF behavior tested.
- Monitoring/security findings and limitations documented.
- Temporary paid resources deleted and remaining billable resources checked.
- Evidence distinguishes completed work from plans and assumptions.
