# Security Requirements

## AWS account and identity
- Enable MFA for root and privileged identities where possible.
- Do not use root for routine administration.
- Prefer IAM roles and temporary credentials over long-lived access keys.
- Apply least privilege; broad administrator permission needs explicit justification.
- Never share access keys, tokens, MFA codes, recovery codes, passwords, or payment information in chat or Git.
- Do not assume the current IAM user can see billing or modify account-level settings.

## Network segmentation
- Separate public, application, database, and management workloads using subnets, route tables, Security Groups, and NACLs.
- Do not expose RDS publicly.
- Do not expose the application EC2 directly to the internet when using an ALB.
- Restrict ALB ingress to required web ports.
- Allow app ingress only from the ALB Security Group where applicable.
- Allow PostgreSQL TCP 5432 only from the application Security Group/source.
- Restrict Windows RDP; never open TCP 3389 to 0.0.0.0/0.
- Security Groups are stateful; NACLs are stateless. Account for ephemeral return traffic.
- Do not confuse network segmentation with Layer 7 WAF filtering.

## Docker and Linux
- Keep Docker and host OS patched.
- Avoid privileged containers unless justified.
- Do not mount Docker socket into app containers.
- Use non-root container users where practical.
- Expose only the proxy/load-balancer port needed.
- Keep application container ports internal to the Docker network where possible.
- Use health checks and inspect logs.
- Two containers on one EC2 are not host-level HA.
- Never store secrets in images, source code, command history, or logs.

## Database
- Set Amazon RDS Publicly accessible = No.
- Enable encryption and TLS where supported/configured.
- Use a dedicated least-privilege application DB account, not the master account.
- Keep credentials outside Git and logs.
- Restrict DB ingress to the application tier.
- Test unauthorized/public database access fails.
- Database replication/DBA HA is out of scope.

## Windows / Microsoft RDS
- Confirm Windows EC2 pricing and Microsoft RDS CAL/licensing requirements.
- Restrict administrative access to a trusted path and authorized source.
- Do not expose RDP to the whole internet.
- Apply Windows updates and review authentication/session policies.
- Treat a single-server RDS setup as a lab, not production HA.

## ALB and WAF
- ALB should be the public entry point; targets should not be directly internet-accessible.
- Use HTTPS for real application traffic; do not send credentials over plain HTTP.
- Test WAF managed rules safely and review false positives.
- WAF is not a substitute for Security Groups, NACLs, host hardening, or network firewalls.

## S3 and backups
- Block public access at account/bucket level as appropriate.
- Enable encryption and restrictive bucket policies.
- Use versioning for recovery exercises where useful.
- Consider Object Lock only after retention/cost review.
- Test restore/recovery, not merely backup creation.

## Public GitHub repository
- Treat every commit as public.
- Never commit credentials, database passwords, private keys, access tokens, sensitive logs, or personal data.
- If a secret is exposed, revoke/rotate it; deleting the file in a later commit is insufficient.
