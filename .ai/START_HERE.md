# Start Here — Handoff Guide

## Read in this order
1. README.md
2. .ai/STATE.md — authoritative current state.
3. .ai/TODO.md — next actions and acceptance criteria.
4. .ai/PROJECT.md
5. Relevant technical docs: ARCHITECTURE, DECISIONS, COST_AND_CLEANUP, SECURITY, RUNBOOK.
6. .ai/SESSION.md — last handoff and exact next action.
7. .ai/CHANGELOG.md

## Mandatory rules
- Never assume a planned action was completed; verify evidence.
- Give direct, step-by-step instructions and only the commands needed for the current step.
- User environment is Windows; Terraform and Ansible are planned for a Linux VM under VMware.
- Before any potentially billable AWS action, explain resource costs, uncertainty, ongoing charges, and exact cleanup steps. Obtain explicit user approval before provisioning.
- Verify AWS credit terms and billing before recommending a plan upgrade or creating resources.
- Prefer least privilege and temporary credentials; do not recommend root access keys for routine work.
- Never ask the user to paste passwords, private keys, MFA codes, payment details, or access keys into chat or Git.
- Terraform state and plans may contain sensitive data. Do not commit them.
- Do not claim a test passed without command output or other evidence.
- After each meaningful session update STATE.md, TODO.md, and SESSION.md. Update other docs when needed.
- Make the next action explicit and small.

## Evidence labels
- Verified: directly confirmed by command output, AWS Console, or repository state.
- User-reported: stated by the user, not independently verified.
- Planned: intended but not performed.
- Not tested: no verification evidence yet.
- Blocked: waiting for a specific issue to be resolved.

## Session closeout
Record changes, commands/results, tests, AWS resources (never secrets), dated cost observations, remaining work, and the exact next action. Commit/push docs when access permits; if remote changes are unavailable, say so clearly.
