# Security Requirements

## AWS account
- Enable MFA for root and privileged identities where possible.
- Do not use root for routine resource administration.
- Prefer IAM roles and temporary credentials over long-lived access keys.
- Apply least privilege; broad admin permission needs explicit justification.
- Never share access keys, tokens, MFA codes, recovery codes, or payment information in chat or Git.
- Do not create public resources without a clear learning need and explicit review.

## Network and host
- Do not expose database ports publicly.
- Restrict SSH to the current public IP when SSH is required.
- Protect private keys with restrictive permissions.
- Keep the OS and packages updated.
- Use non-root service accounts where practical.
- Do not use production or sensitive personal data in the lab.

## Database
- Bind to localhost/private interfaces as required.
- Create a dedicated application database and non-admin user.
- Store generated passwords outside Git.
- Test that unauthorized/public database access fails.
- Avoid credentials in command-line arguments where shell history or process listings may expose them.

## Terraform
- Never commit tfstate, state backups, secret-bearing tfvars, or plan files.
- Treat state and plans as sensitive.
- Never commit AWS credentials.
- Review every planned resource before applying.
- Avoid scripts that print secrets.

## Ansible
- Use Ansible Vault or an approved secret manager if needed; never commit vault passwords.
- Use no_log for tasks that might expose secrets.
- Prefer idempotent tasks and explicit privilege escalation.
- Do not permanently disable host-key checking for convenience.

## Public repository
The repository is public at last inspection. Treat every commit as public. If a secret is exposed, revoke/rotate it; deleting the file in a later commit is not sufficient. Follow GitHub's sensitive-data remediation guidance.
