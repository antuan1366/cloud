# Six-Day Secure Cloud Operations Lab

Last updated: 2026-10-31  
Status: Proposed plan only. No resources for this revised architecture have been deployed.

## Goals and constraints

- Configure AWS infrastructure through the AWS Management Console.
- Do not use Terraform or AWS CLI to deploy this iteration.
- Remove Nginx.
- Use one Linux EC2 host running Docker: two application containers plus one HAProxy or Traefik container.
- Include one private Amazon RDS PostgreSQL instance, initially Single-AZ.
- Exclude database replication and DBA-focused HA.
- Include one Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Learn VPC segmentation, Security Groups, NACLs, ALB, WAF, S3, IAM, logging, and security assessment.
- The previously reported USD 120 credit and 2026-11-05 deadline must be rechecked in the account.
- Explain costs and obtain explicit approval before every potentially billable deployment or paid feature activation.

## 1. Proposed architecture

Use one VPC with CIDR 10.10.0.0/16, four logical security zones, and two Availability Zones.

### Security zones and subnet proposal

| Zone | Subnets | Intended resources | Exposure |
|---|---|---|---|
| Public | Public-A, Public-B | Internet-facing ALB | ALB listeners only |
| Application | Private-App-A, Private-App-B | One Linux EC2 running Docker | No direct internet inbound |
| Database | Private-DB-A, Private-DB-B | Amazon RDS DB subnet group | No public access |
| Management | Private-Management-A | Windows Server / Microsoft RDS lab | Restricted administration path |

Illustrative subnet ranges (confirm no overlap before creation):
- Public-A: 10.10.1.0/24; Public-B: 10.10.2.0/24
- Private-App-A: 10.10.11.0/24; Private-App-B: 10.10.12.0/24
- Private-DB-A: 10.10.21.0/24; Private-DB-B: 10.10.22.0/24
- Private-Management-A: 10.10.31.0/24

Security zones are logical trust areas implemented through subnet placement, route tables, Security Groups, NACLs, and potentially firewalls. Availability Zones are separate AWS infrastructure locations in a Region. These concepts are not interchangeable.

### Planned resources

| Resource | Quantity | Purpose |
|---|---:|---|
| Linux EC2 | 1 × t3.medium (provisional) | Docker host |
| Application containers | 2 | Demonstrate application replicas |
| HAProxy or Traefik container | 1 | Load balance between app containers |
| Windows Server EC2 | 1 | Microsoft Remote Desktop Services learning |
| Amazon RDS PostgreSQL | 1, Single-AZ initially | Managed database exercise |
| Application Load Balancer | 1, temporary | AWS-managed traffic distribution |
| AWS WAF | 1 Web ACL, temporary | HTTP/HTTPS filtering |
| S3 bucket | 1 | Private object storage / backup / log exercise |
| Security Groups and NACLs | Several | Network access control |

No Nginx.

### Docker and AWS load balancing are different

The Docker proxy distributes requests between two containers on the same EC2 host. It teaches container networking, health checks, and reverse proxying. It does not provide EC2-level or AZ-level high availability because all containers share one host.

The AWS Application Load Balancer is a separately billed managed AWS service. It is a distinct Day 5 exercise. With only one EC2 target, it does not make the application highly available.

## 2. Intended traffic policy

| Source | Destination | Intended access |
|---|---|---|
| Internet | ALB | HTTPS 443; HTTP 80 only if needed for redirect/testing |
| ALB | Application EC2 | Application target port only |
| Application EC2 | RDS | PostgreSQL TCP 5432 |
| Management host | Application EC2 | Only required administration |
| Internet | RDS | Deny |
| Internet | Application EC2 directly | Deny |
| Untrusted internet | Windows RDP 3389 | Deny |

Security Groups are stateful and attached to resources/network interfaces. NACLs are stateless and apply at subnet boundaries; account for return traffic and ephemeral ports. Neither replaces a Layer 7 WAF.

The base lab does not require Transit Gateway or a dedicated inspection VPC. Centralized inspection with Transit Gateway, AWS Network Firewall, FortiGate-VM, F5, or FortiWeb can be a later exercise after pricing and routing are reviewed.

## 3. Amazon RDS

Deploy one PostgreSQL RDS instance in private DB subnets, initially Single-AZ:
- Public accessibility disabled.
- Encryption enabled.
- DB subnet group spanning private subnets in two AZs.
- PostgreSQL ingress only from the approved application Security Group/source.
- Dedicated least-privilege application database account.
- Backup retention selected after price review.

No database replication, multi-instance design, or DBA HA is in scope.

## 4. Microsoft Remote Desktop Services

Amazon RDS means Relational Database Service. Microsoft RDS means Remote Desktop Services; they are unrelated.

Use one Windows Server EC2 for learning. RD Session Host, RD Gateway, RD Web Access, Connection Broker, and RD Licensing are distinct roles/components. A single-server lab is not a production RDS farm.

Before launch:
- Confirm Windows EC2 pricing and Microsoft RDS CAL/licensing requirements.
- Select a secure path to the private Windows host, such as a reviewed Session Manager port-forwarding design, VPN, or tightly restricted temporary RDP source rule.
- Never expose TCP 3389 to the entire internet.
- Do not claim production HA from one Windows instance.

## 5. Storage decisions

- EBS: block storage for EC2 operating systems and attached data.
- S3: private object storage for small backup/log exercises; configure encryption and restrictive bucket policy, optionally versioning.
- RDS automated backups: database recovery mechanism.
- EFS: optional only; not required for a stateless/containerized application. EFS is shared NFS storage, not server-to-server replication.
- Veeam is out of initial scope pending licensing, architecture, and cost review.

## 6. Six-day schedule

### Day 1 — VPC, subnets, routing, and access controls
- Recheck account, Region, credits, billing visibility, and existing resources.
- Inspect the previous Terraform-managed EC2 lab before adding anything.
- Create one VPC and public, application, database, and management subnets only after cost review and approval.
- Configure Internet Gateway and route tables.
- Create tier-specific Security Groups and NACLs.
- Validate permitted and denied traffic.
- Acceptance: network diagram, subnet/route-table inventory, and tested access policy.

### Day 2 — Linux EC2 and Docker
- Launch one Linux EC2 only after cost approval.
- Install Docker.
- Deploy two application containers and one HAProxy or Traefik container.
- Configure internal Docker networking and health checks.
- Test request distribution and stop one app container to observe behavior.
- Acceptance: application reachable through Docker proxy; logs and failure behavior recorded.
- Limitation: not host-level HA.

### Day 3 — Amazon RDS PostgreSQL and S3
- Create a DB subnet group using private DB subnets in two AZs.
- Deploy a small Single-AZ PostgreSQL RDS instance with Public access disabled and encryption enabled.
- Restrict database ingress to the application Security Group/source.
- Connect the app using a dedicated least-privilege DB account; keep credentials out of Git and logs.
- Create one private S3 bucket; configure encryption, access policy, and optionally versioning.
- Test unauthorized DB/S3 access and object recovery.
- Acceptance: app-to-RDS connectivity works; unauthorized access fails; S3 is not public.
- No DB replication/failover exercise.

### Day 4 — Windows Server and Microsoft RDS
- Review Windows EC2 price and Microsoft RDS CAL/licensing requirements.
- Choose a secure administration path; do not expose RDP to all sources.
- Launch one Windows Server EC2 after cost approval.
- Learn and configure only the minimum RDS role(s) needed.
- Review Windows event logs and session policies.
- Acceptance: authorized remote administration works; unauthorized RDP paths are blocked; single-server limitation documented.

### Day 5 — ALB, WAF, and firewalling
- Review ALB and WAF pricing before creation.
- Create temporary ALB in two public subnets.
- Register the Linux EC2 target and configure health checks.
- Attach a WAF Web ACL with selected managed rules.
- Test safe representative SQL injection/XSS strings and inspect WAF metrics/logging.
- Compare F5 Advanced WAF and FortiWeb conceptually; do not deploy licensed appliances without separate trial and cost review.
- Explain AWS Network Firewall/FortiGate-VM placement and cost.
- Acceptance: ALB target health and WAF behavior verified. One target does not provide application HA.

### Day 6 — Monitoring, security assessment, and cleanup
- Review CloudTrail Event History and CloudWatch.
- Review GuardDuty, Security Hub, and Inspector pricing before activation.
- Run Prowler, Checkov, or Trivy only after reviewing scope, permissions, and execution costs.
- Review IAM, Security Groups, NACLs, public exposure, encryption, and S3 policy.
- Save non-sensitive results.
- Delete temporary ALB/WAF and other resources no longer needed; stop or delete compute/database resources according to data-retention decision.
- Verify remaining resources in all relevant Regions and check billing after usage data updates.
- Acceptance: no unintended lab resources remain; findings and cost observations documented.

## 7. Cost guardrails

The USD 120 credit and 2026-11-05 access deadline are user-reported and must be rechecked. Credit eligibility varies by account and service; never assume all usage is covered.

Before each deployment:
1. Confirm account, Region, existing resources, current credit balance, expiry, and eligible services.
2. Check exact current pricing for instance size, runtime, storage, public IP, data transfer, request volume, and dependent services.
3. Explain charges while running, stopped, or idle.
4. Identify resources that must be deleted to stop hourly charges.
5. Obtain explicit user approval.

Important:
- Stopping EC2 stops compute charges but EBS storage and some networking/public IPv4 charges can remain.
- Stopping RDS does not stop storage/backup charges; AWS automatically restarts an RDS instance after seven consecutive days stopped.
- ALB, WAF, NAT Gateway, and AWS Network Firewall can charge independently of stopped EC2 targets.
- Avoid NAT Gateway and AWS Network Firewall in the base lab unless explicitly approved after price review.
- Budget alerts are notifications, not hard spending caps; billing data can be delayed.
- A six-day schedule does not guarantee total spend below USD 120.

## 8. Explicit exclusions

- No Nginx.
- No database replication, DBA failover, or database HA engineering.
- No claim of EC2/application HA from two containers on one host.
- No production Microsoft RDS farm or multi-server RDS HA.
- No Transit Gateway or dedicated inspection VPC in the base single-VPC lab.
- No paid firewall appliance deployment without separate licensing and cost review.
- No Terraform or AWS CLI for infrastructure deployment in this iteration.

## 9. Operating rules

- Console-first AWS infrastructure configuration.
- Terminal commands inside EC2 may be used for Docker and OS configuration; explain commands before execution.
- Never request secrets, passwords, private keys, MFA codes, or access keys in chat.
- Do not commit credentials, database passwords, private keys, Terraform state, or sensitive logs.
- Distinguish planned work from verified deployment.
- Obtain user approval before potentially billable actions.
- Update this repository only when the user explicitly asks.
