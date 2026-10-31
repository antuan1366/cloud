# Architecture

Status: proposed; the revised six-day environment has not been deployed.

## Design summary
Use one VPC with logical public, application, database, and management security zones distributed across two Availability Zones. Illustrative VPC CIDR: 10.10.0.0/16.

| Zone | Subnets | Workloads |
|---|---|---|
| Public | Public-A, Public-B | Internet-facing ALB |
| Application | Private-App-A, Private-App-B | One Linux EC2 Docker host |
| Database | Private-DB-A, Private-DB-B | Amazon RDS DB subnet group |
| Management | Private-Management-A | Windows Server / Microsoft RDS lab |

Illustrative subnet ranges:
- Public-A 10.10.1.0/24; Public-B 10.10.2.0/24
- Private-App-A 10.10.11.0/24; Private-App-B 10.10.12.0/24
- Private-DB-A 10.10.21.0/24; Private-DB-B 10.10.22.0/24
- Private-Management-A 10.10.31.0/24

Confirm CIDR non-overlap and AZ availability before creation.

## Application tier
One Linux EC2 (provisional t3.medium) runs Docker:
- Application container A.
- Application container B.
- One HAProxy or Traefik container for internal container load balancing.

Nginx is explicitly removed.

The Docker proxy distributes requests between two containers on the same EC2 host. It teaches container networking, health checks, and proxying; it does not provide EC2 host-level or AZ-level HA. If the EC2 instance fails, all containers on it fail together.

A separate AWS Application Load Balancer is a temporary Day 5 exercise. It has independent hourly and capacity-unit charges. With only one EC2 target, it does not make the application highly available.

## Database tier
One Amazon RDS for PostgreSQL instance, Single-AZ initially:
- DB subnet group spans private subnets in at least two AZs.
- Public accessibility disabled.
- Encryption enabled.
- Database port allowed only from the approved application Security Group/source.
- Dedicated least-privilege application DB user.
- Backup retention selected after cost review.

No PostgreSQL replication, multi-instance design, or DBA HA is in scope.

## Management tier
One Windows Server EC2 for Microsoft Remote Desktop Services learning.

Microsoft RDS (Remote Desktop Services) is unrelated to Amazon RDS (Relational Database Service). RD Session Host, RD Gateway, RD Web Access, Connection Broker, and RD Licensing are distinct roles/components.

A single-server setup is for learning only. Confirm Windows EC2 price and Microsoft RDS CAL/licensing requirements. Do not expose TCP 3389 to the world. Choose a secure path to the private host before deployment, such as a reviewed Systems Manager port-forwarding setup, VPN, or tightly restricted temporary RDP source rule.

## Storage
- EBS: block storage for EC2 operating system and attached data.
- S3: private object storage for backup/log demonstrations; configure encryption, restrictive bucket policy, and optional versioning.
- RDS automated backups: database recovery mechanism.
- EFS: optional, not required for the stateless/containerized application. EFS is shared NFS file storage, not server-to-server replication.
- Veeam is out of initial scope pending licensing and cost review.

## Network security
Security Groups are stateful and attached to resources/network interfaces. NACLs are stateless subnet-level controls; return and ephemeral traffic must be considered.

Intended traffic:
- Internet -> ALB: HTTPS 443 (HTTP 80 only if needed for redirect/testing).
- ALB -> app EC2: application target port only.
- App EC2 -> RDS: PostgreSQL 5432 only.
- Management -> app EC2: only required administration.
- Internet -> RDS: denied.
- Internet -> app EC2 directly: denied.
- Untrusted internet -> Windows RDP 3389: denied.

One VPC is sufficient for the base lab. Transit Gateway and a dedicated inspection VPC are advanced follow-up subjects, not required here. A firewall appliance or AWS Network Firewall needs deliberate routing and a separate cost review.

## Deployment method
For this iteration, AWS infrastructure is configured in the AWS Management Console. Do not use Terraform or AWS CLI to deploy the environment. Terminal commands inside EC2 may be used for Docker and OS configuration, with explanations and cost review where relevant.

## Previous lab
A previous Terraform/Ansible exercise deployed a small EC2/Nginx web server. Inspect it in the AWS Console before creating the new environment. Do not assume it is still running, and do not delete it without explicit user approval.
