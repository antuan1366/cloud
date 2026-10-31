# Current State

Last updated: 2026-10-31  
Status: Architecture and six-day implementation plan revised; new scenario resources have not been deployed.

## Current direction
- User explicitly requested AWS Management Console configuration for the new scenario, not Terraform or AWS CLI deployment.
- One VPC with logical public, application, database, and management security zones.
- Two Availability Zones for subnet and managed-service learning.
- One Linux EC2 host running Docker: two application containers plus one HAProxy or Traefik container.
- Nginx removed from the design.
- One private Amazon RDS PostgreSQL instance, initially Single-AZ. Database replication/DBA HA is out of scope.
- One Windows Server EC2 for Microsoft Remote Desktop Services learning.
- Temporary ALB and AWS WAF exercises.
- One private S3 bucket for storage/backup/log exercises.
- No Transit Gateway or dedicated inspection VPC in the base architecture.
- Detailed daily tasks: .ai/IMPLEMENTATION_PLAN_6_DAYS.md.

## Previous learning exercise — historical verified results
The earlier lab used Terraform and Ansible and was deployed before the current console-first redesign:
- A t3.micro Amazon Linux 2023 EC2 web server was provisioned in us-east-1.
- Terraform created an EC2 instance, key pair, and Security Group.
- Ansible installed and started Nginx.
- The web endpoint returned HTTP 200.
- Previously recorded instance ID: i-05cd787404265bc18.
- Previously recorded public IP: 54.163.28.219.
- These are historical details, not a fresh check of current AWS state. Inspect the AWS Console before creating anything else. Do not assume the instance is still running or safe to delete.
- The previous lab source and Terraform state may exist on the user's Ubuntu VM. Do not overwrite or destroy it without explicit approval.

## Local tooling — previously verified
- Ubuntu VM hostname shown as juniper; normal user antuan.
- Ubuntu 24.04.5 LTS.
- Git 2.43.0; Terraform v1.17.0; AWS CLI v2.38.6; Python 3.12.3.
- Ansible core 2.21.5 in /home/antuan/ansible-venv; system Ansible 2.16.3 also exists.
- These tools remain available for learning, but Terraform/AWS CLI are not to be used for infrastructure deployment in the current scenario.

## AWS account context — user-reported, not freshly verified
- AWS Console is accessible.
- Credits page previously showed USD 120 remaining.
- Access/free-plan message previously said access ends on 5 November 2026 or when credits are depleted.
- User previously used an IAM user named adel and may not have billing permissions.
- Current credit balance, eligible services, usage, billing, account access type, MFA, Region, and resource inventory must be rechecked.

## Not yet done for revised scenario
- No new VPC/subnets/security zones have been created.
- No Docker host/containers have been deployed.
- No new Amazon RDS database has been created.
- No Windows RDS server has been created.
- No ALB or WAF has been created.
- No S3 bucket has been created.
- No new firewall appliance or AWS Network Firewall has been deployed.
- No new GuardDuty, Security Hub, or Inspector activation has been approved.

## Immediate next action
1. Inspect the existing EC2 instance and related resources in the AWS Console.
2. Recheck credit balance, expiry, eligible services, current usage, billing visibility, Region, and account permissions.
3. Decide whether to retain or clean up the previous lab. Do not delete it without explicit user approval.
4. Confirm exact pricing and dependencies for Day 1 networking and proposed EC2/RDS/Windows/ALB/WAF exercises.
5. Present a cost warning and obtain explicit approval before creating resources.

## Update policy
Only update this repository when the user explicitly asks. Replace stale values when newer evidence arrives. Date balances, deadlines, inventory checks, and test results.
