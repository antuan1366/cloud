# AWS Cost and Cleanup Controls

## Baseline (user-reported; recheck live)
- Credits: USD 120.00.
- Console message: free access ends on 2026-11-05 or when credits are depleted.
- The console previously showed 13 days remaining; this relative count is time-sensitive.
- Current bill, usage, eligible services, and post-deadline plan behavior are unknown.

## Required pre-deployment check
Before terraform apply, manual AWS creation, or a plan upgrade:
1. Verify current credit balance, expiry, eligible services, and plan terms.
2. Check intended region and current billing/usage.
3. List every resource the action will create.
4. Check current official prices and dependencies.
5. Explain charges while running, stopped, or idle.
6. Explain exact cleanup steps, including resources not removed automatically.
7. Present estimates as estimates, not guarantees.
8. Obtain explicit user approval before creating resources.

## Cost risks to investigate
Actual prices depend on region, configuration, usage, and current terms. Check current pricing.
- EC2 runtime.
- EBS volumes and snapshots.
- Public IPv4 and other networking.
- Data transfer.
- RDS runtime, storage, backups, snapshots if used.
- NAT Gateway hourly/data processing.
- Load balancers.
- CloudWatch logs/metrics beyond included allowances.
- Route 53 zones/domains if added.
- Services excluded from promotional credits.

Avoid NAT Gateway, load balancer, and always-on RDS initially unless approved after review.

## Budget caveat
Budgets and billing alerts notify; they are not hard spending caps. Billing data can be delayed.

## Cleanup checklist
Before:
- [ ] Save needed documentation and test results.
- [ ] Confirm data can be discarded.
- [ ] Inspect Terraform workspace/state and the destroy plan.
- [ ] Confirm state targets only this lab.

During:
- [ ] Review terraform destroy plan and obtain user approval.
- [ ] Do not delete shared or unrelated resources.
- [ ] Record output and errors.

After:
- [ ] Inspect EC2 instances and EBS volumes.
- [ ] Inspect snapshots and AMIs.
- [ ] Inspect public IPv4/Elastic IP resources, load balancers, NAT Gateways, RDS, and other created resources.
- [ ] Inspect metered log groups or services if created.
- [ ] Check every relevant region.
- [ ] Recheck Billing/credits after usage data updates.
- [ ] Update STATE.md and SESSION.md.

Stopping EC2 does not necessarily stop charges for storage, snapshots, public IPv4, or other resources. Deleting an instance can leave separate resources behind.
