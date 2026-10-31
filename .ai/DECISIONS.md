# Decision Log

## D-001 — GitHub is the portable project record
Date: 2026-10-25 | Status: Accepted  
Store state, tasks, architecture, decisions, cost notes, runbooks, and handoff in this repository.

## D-002 — Console-first deployment for current scenario
Date: 2026-10-31 | Status: Accepted  
Use the AWS Management Console for infrastructure deployment in this iteration. Terraform/AWS CLI remain installed for prior learning but are not used to deploy this scenario.

## D-003 — Inspect previous lab before expansion
Date: 2026-10-31 | Status: Accepted  
Inspect the earlier Terraform-managed EC2 and related resources in the Console before creating anything new. Do not delete without explicit approval.

## D-004 — One VPC with logical security zones
Date: 2026-10-31 | Status: Proposed architecture accepted  
Use public, application, database, and management zones distributed across two AZs. Separate VPCs and Transit Gateway are unnecessary for the base lab.

## D-005 — One Docker host with internal container load balancing
Date: 2026-10-31 | Status: Proposed architecture accepted  
Use one Linux EC2 with two app containers and one HAProxy or Traefik container. Remove Nginx. This teaches container networking but does not provide EC2/AZ HA.

## D-006 — Amazon RDS PostgreSQL without database HA scope
Date: 2026-10-31 | Status: Proposed architecture accepted  
Use one private Single-AZ RDS PostgreSQL instance. Database replication and DBA HA are out of scope.

## D-007 — Microsoft Remote Desktop Services learning
Date: 2026-10-31 | Status: Proposed architecture accepted  
Use one Windows Server EC2 for Microsoft RDS role learning. Confirm Windows pricing and Microsoft RDS CAL/licensing requirements. Do not expose RDP publicly without tight restriction.

## D-008 — Temporary ALB and WAF exercises
Date: 2026-10-31 | Status: Proposed architecture accepted  
Create ALB/WAF only for their exercise, after pricing review; delete afterward if no longer needed.

## D-009 — Cost warning and approval
Date: 2026-10-25 | Status: Accepted  
Explain costs, uncertainty, ongoing charges, and cleanup before potentially billable actions. Obtain explicit approval before provisioning or enabling paid services.

## D-010 — No secrets in Git
Date: 2026-10-25 | Status: Accepted  
Never commit credentials, keys, database passwords, Terraform state, sensitive logs, or secret-bearing variable files.

## D-011 — Exclusions
Date: 2026-10-31 | Status: Accepted  
No Nginx, DB replication/DBA HA, Transit Gateway, dedicated inspection VPC, or paid firewall appliance in the base lab. These may be future advanced topics after separate review.
