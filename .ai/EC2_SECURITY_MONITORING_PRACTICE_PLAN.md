# EC2 Security, Disk Monitoring, and Email Automation Practice Plan

Last updated: 2026-11-04  
Status: Planned practice track. No new AWS resources or monitoring configuration have been deployed for this scenario.

## Purpose

Prepare for a practical AWS infrastructure task covering EC2 hardening, filesystem capacity monitoring, CloudWatch dashboards, threshold-based email alerts, and scheduled storage reports.

This track is based on an Upwork job description reviewed on 2026-11-04. It is a learning and portfolio exercise, not evidence of prior production delivery.

## Job requirement fit and current gaps

| Job requirement | Existing foundation | Practice gap |
|---|---|---|
| EC2 security review | Networking, infrastructure security, vulnerability-management and Linux/Windows background | Demonstrate a repeatable EC2 hardening checklist and before/after evidence |
| Security Groups and NACLs | Existing VPC/security-group learning | Rehearse least-privilege ingress/egress and stateless NACL return traffic |
| SSH restrictions and key authentication | Linux and networking foundation | Restrict SSH to a trusted source; validate key-based access and safer Systems Manager access where feasible |
| OS patches and updates | Windows/Linux administration | Demonstrate patch assessment, controlled installation, reboot planning, and verification |
| IAM roles and permissions | General IAM familiarity; AWS lab experience | Attach a least-privilege EC2 instance role for CloudWatch Agent; understand trust and permissions |
| Vulnerability review | Nessus/OpenVAS experience | Connect host-level findings to EC2 exposure and document remediation/retest |
| CPU and network monitoring | Standard EC2 metrics are available | Build and interpret a CloudWatch dashboard |
| RAM and disk monitoring | Not yet demonstrated in this lab | Install/configure CloudWatch Agent and validate memory/filesystem metrics |
| Disk capacity totals and percentages | Linux/Windows administration foundation | Identify filesystem dimensions and report total, used, free, and utilization accurately |
| 80%/90% disk email alerts | Not yet demonstrated | Configure CloudWatch alarms and SNS email subscriptions; test state transitions |
| Daily/weekly storage report | Scripting and AWS automation are learning areas | Build a scheduled report workflow, likely Lambda + EventBridge + SNS, and validate every reported field |

## Target learning architecture

- EC2 Linux and, as an optional extension, Windows.
- CloudWatch Agent on each monitored instance to publish memory and filesystem metrics.
- CloudWatch metrics and dashboards for CPU, network, memory, and disk utilization.
- CloudWatch alarms for agreed disk thresholds (for example, warning at 80% and critical at 90%).
- Amazon SNS email subscription for alert delivery.
- A scheduled reporting component (for example, EventBridge schedule invoking Lambda) to collect instance/filesystem metrics and send a daily or weekly storage summary.

Important distinctions:
- EC2 publishes basic CPU and network metrics by default; guest memory and filesystem metrics require an agent or another collection mechanism.
- A dashboard visualizes metrics; it does not by itself send notifications.
- A CloudWatch alarm detects a metric condition; SNS delivers the notification.
- A threshold alert is not the same as a periodic inventory report. A report listing server name, total, used, available, and percentage may require aggregation and formatting logic.
- Filesystem metrics can have separate dimensions for mount point, device, and filesystem type. The report must avoid accidentally combining or omitting volumes.
- Linux and Windows agent configuration and filesystem naming differ. Start with one OS, then extend to the other only after the first is verified.

## Prerequisites

### Knowledge
- EC2 lifecycle, AMIs, instance profiles, IAM roles and policies.
- Security Groups versus NACLs; stateful versus stateless filtering.
- SSH key authentication and secure Windows administration.
- Basic Linux or Windows patching and service management.
- CloudWatch metrics, namespaces, dimensions, alarms, dashboards, and SNS.
- Basic scripting and JSON configuration.
- Lambda execution role, EventBridge schedule, and SNS publish permissions for the scheduled-report extension.

### Access and tools
- Authorized AWS account and a defined Region.
- Permission to inspect EC2, IAM, CloudWatch, SNS, and (for the report extension) Lambda and EventBridge.
- A test email address that the user controls for SNS subscription confirmation.
- One disposable or approved EC2 test instance; inspect existing resources before creating another.
- CloudWatch Agent package and configuration appropriate to the selected operating system.
- No credentials, private keys, or sensitive instance data in GitHub.

### Cost and safety gate
Before deploying or enabling anything, recheck account credits, expiry, service eligibility, Region, existing resources, and current pricing.
Potential charges can include EC2 runtime, EBS storage, public IPv4, CloudWatch custom metrics and alarms, log ingestion/storage, dashboards, SNS usage, Lambda invocations, and EventBridge schedules. Exact costs depend on Region, metric count, reporting frequency, retention, and runtime.
Do not assume promotional credits cover every service. Explain the expected charges and cleanup steps and obtain explicit user approval before any potentially billable AWS action. No resource creation is authorized by this document.

## Practice sequence and acceptance criteria

### Phase 1 — EC2 security baseline
- Inventory the test instance, OS, attached volumes, network interfaces, public exposure, and IAM instance profile.
- Review Security Groups and NACLs; remove unnecessary inbound access.
- Restrict SSH to a trusted source or prefer Systems Manager Session Manager where supported and configured.
- Verify key-based SSH access; do not expose port 22 to the world.
- Review local firewall, listening ports, running services, patch status, and administrative access.
- Attach only the permissions required by the CloudWatch Agent.
- Record findings, remediation, and retest evidence.

Acceptance: a concise hardening checklist is completed; intended administration works; unapproved access paths are blocked; changes and limitations are documented.

### Phase 2 — CloudWatch Agent metrics
- Install the CloudWatch Agent on one Linux EC2 instance first.
- Configure memory utilization and filesystem metrics, plus any required disk capacity metrics.
- Verify metrics arrive in the expected namespace with correct instance and filesystem dimensions.
- Compare CloudWatch values with OS-native commands to validate units and accuracy.
- Document metric interval, dimensions, and any filesystem exclusions.
- Add Windows only as a separate extension after Linux acceptance.

Acceptance: CPU/network and agent-provided memory/disk metrics are visible and cross-checked against the operating system.

### Phase 3 — Dashboard
- Create a dashboard showing instance identity, CPU, network traffic, memory utilization, and filesystem utilization.
- Include clear labels and units; distinguish multiple disks/mount points.
- Test behavior when a metric is missing or an instance is stopped.

Acceptance: a reviewer can identify the host and see its current and historical resource trends without confusing filesystems.

### Phase 4 — Email threshold alerts
- Create warning and critical disk alarms (for example 80% and 90%).
- Configure SNS email delivery and confirm the subscription.
- Test alarm state transitions safely; do not fill a production disk to force an alarm.
- Confirm alert content identifies the instance and filesystem where possible.
- Document alarm evaluation periods, missing-data behavior, and reset/OK notifications.

Acceptance: controlled test data causes the expected alarm transition and a confirmed email reaches the test inbox.

### Phase 5 — Scheduled storage reports
- Define whether reports are daily or weekly and which instances/filesystems are in scope.
- Build a scheduled workflow, provisionally EventBridge → Lambda → CloudWatch metric retrieval/aggregation → SNS email.
- Include server name/instance ID, filesystem or volume, total capacity, used capacity, available capacity, utilization percentage, and report timestamp.
- Handle missing metrics, stopped instances, multiple filesystems, and partial failures explicitly.
- Validate calculations against OS-native values before relying on the report.

Acceptance: a scheduled test report is received and all capacity figures reconcile with the test host. Document limitations and error handling.

### Phase 6 — Evidence and portfolio handoff
- Save sanitized architecture, configuration excerpts, dashboard screenshots, alarm test evidence, sample report, and hardening checklist.
- Record the exact OS, agent version, metric names/dimensions, thresholds, and tested behavior.
- Include a cleanup record and cost observations.
- State clearly that this is a lab implementation, not production client delivery.

Acceptance: another engineer can understand, reproduce, validate, and safely clean up the exercise.

## Security tips

- Sec-Tip1: Never allow SSH (TCP/22) from 0.0.0.0/0 for routine administration; restrict source addresses or use Systems Manager Session Manager. Reference: AWS EC2 security best practices; NIST SP 800-53 AC-17.
- Sec-Tip2: Attach an IAM role to EC2 and grant only the permissions needed to publish the required telemetry. Avoid long-lived access keys on the instance. Reference: AWS IAM best practices; ISO/IEC 27001:2022 access-control themes.
- Sec-Tip3: Treat monitoring configuration as security-sensitive: protect dashboards, log groups, alarm actions, and report recipients from unauthorized modification. Reference: AWS Well-Architected Security Pillar; NIST SP 800-53 AU-2/AU-6.
- Sec-Tip4: Disk alerts are operational controls, not a substitute for capacity planning, backups, or recovery testing. Reference: AWS Well-Architected Reliability Pillar.

## Out of scope for this practice track

- Production fleet-scale monitoring or enterprise observability architecture.
- Auto-remediation that resizes volumes or deletes files automatically.
- Claims of production experience based solely on this lab.
- Deploying resources before cost review and explicit user approval.

## References

- CloudWatch Agent: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html
- CloudWatch Agent configuration: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-Configuration-File-Details.html
- CloudWatch alarms: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html
- SNS email subscriptions: https://docs.aws.amazon.com/sns/latest/dg/sns-email-notifications.html
- EventBridge Scheduler: https://docs.aws.amazon.com/scheduler/latest/UserGuide/what-is-scheduler.html
- AWS Lambda: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html
- EC2 security best practices: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html
- IAM best practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- NIST SP 800-53: https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final

## Completion criteria

The learner can independently harden a small EC2 deployment, collect and validate CPU/network/memory/filesystem metrics, build a usable CloudWatch dashboard, configure and test email threshold alerts, generate a scheduled capacity report with accurate per-filesystem values, explain the IAM permissions and cost model, and produce sanitized reproducible evidence.
