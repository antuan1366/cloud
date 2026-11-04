# Cloud Infrastructure Auditing Learning Plan

Status: Planned learning track. No audit has been performed and no compliance opinion or certification is offered.

## Purpose

Develop practical skills to assess the security and operational posture of AWS environments, identify misconfigurations and control gaps, collect defensible technical evidence, recommend remediation, and verify fixes.

This is a technical cloud-infrastructure assessment and audit-readiness learning track. It does not train the learner to issue an independent SOC 2 report or act as a CPA firm.

## Learning outcomes

By completing this track, the learner should be able to:

1. Define an assessment scope, authorization boundaries, assumptions, and exclusions.
2. Inventory AWS accounts, Regions, workloads, identities, network paths, data stores, and security services.
3. Assess IAM, network exposure, encryption, logging, monitoring, backup, vulnerability management, and change controls.
4. Compare observed configurations with recognized security baselines.
5. Collect and protect evidence without exposing credentials, personal data, or sensitive customer information.
6. Write clear findings with risk, business impact, evidence, and actionable remediation.
7. Retest remediated controls and produce a concise technical assessment report.
8. Map technical evidence to selected ISO/IEC 27001, NIST, CIS AWS Foundations Benchmark, and SOC 2 Trust Services Criteria topics without claiming the frameworks are interchangeable.

## Prerequisites

- Understand AWS accounts, Regions, VPCs, subnets, route tables, Security Groups, and NACLs.
- Understand IAM users, roles, policies, MFA, and least privilege.
- Understand EC2, S3, RDS, CloudTrail, CloudWatch, and basic backup concepts.
- Be comfortable reading security findings and explaining remediation.
- Understand Linux, networking, and basic Git.
- Use a dedicated lab account/environment where possible. Confirm permissions and cost before enabling paid services or running tools.

## Assessment workflow

### Phase 1 — Scope and authorization

- Identify the account, Regions, environments, business services, and data types in scope.
- Obtain written authorization and confirm whether the work is read-only or includes configuration changes.
- Define test windows, prohibited actions, contacts, evidence handling, and reporting expectations.
- Record exclusions and limitations.
- Never scan or test an account, workload, or external target without authorization.

Deliverable: assessment scope and rules of engagement.

### Phase 2 — Asset and architecture discovery

- Inventory AWS accounts and enabled Regions.
- Identify VPCs, subnets, route tables, internet gateways, NAT gateways, endpoints, Security Groups, and NACLs.
- Identify compute, containers, databases, storage, load balancers, and exposed endpoints.
- Review identity providers, IAM principals, roles, policies, and cross-account access.
- Draw a current-state architecture and data-flow diagram.

Deliverable: asset inventory, architecture diagram, and attack-surface summary.

### Phase 3 — Control assessment

Assess at least these domains:

| Domain | Example checks | Example evidence |
|---|---|---|
| Identity and access | MFA, root account protection, least privilege, stale credentials, role trust policies, access reviews | IAM configuration, credential report, Access Analyzer findings, review records |
| Network security | Public exposure, permissive ingress, segmentation, admin access paths, routing | VPC/subnet/route tables, Security Groups, NACLs, architecture diagram |
| Data protection | Encryption, public S3 access, key policies, database exposure, secrets handling | S3 Block Public Access, bucket policies, encryption settings, KMS configuration |
| Logging and monitoring | CloudTrail coverage, log integrity/retention, alerting, audit log access | Trail configuration, CloudWatch alarms/log groups, log bucket policy |
| Vulnerability management | Findings, severity, ownership, remediation SLA, retest | Inspector or approved scanner findings, tickets, remediation evidence |
| Configuration management | Baselines, drift, approved changes, deletion protection | AWS Config rules/history, change records, resource settings |
| Backup and recovery | Backup coverage, retention, restore tests, RTO/RPO | Backup plans, recovery points, restore-test record, recovery procedure |
| Incident response | Detection, escalation, response ownership, lessons learned | Runbooks, alert examples, incident exercise records |
| Availability and resilience | Single points of failure, health checks, failover design, capacity risks | Architecture, health checks, recovery tests, monitoring |

Do not assume a service is compliant merely because it is enabled. Evaluate configuration, coverage, operation, and evidence.

### Phase 4 — Baselines and framework mapping

Use the following as references, selecting only controls relevant to the defined scope:

- CIS AWS Foundations Benchmark for AWS-specific configuration recommendations.
- AWS Well-Architected Framework, especially the Security and Reliability pillars.
- NIST Cybersecurity Framework for governance, identification, protection, detection, response, and recovery outcomes.
- ISO/IEC 27001:2022 for information-security management system context and relevant Annex A controls.
- SOC 2 Trust Services Criteria for technical control themes when the client's audit-readiness scope requires it.

Create a mapping matrix with columns:
- Assessment ID
- Observed AWS resource/control
- Baseline or framework reference
- Expected state
- Actual state
- Evidence reference
- Result (Pass / Gap / Not Applicable / Not Tested)
- Risk rating
- Recommended action
- Owner
- Retest status

Framework mappings are contextual, not automatic equivalences. A technical configuration check alone does not prove that an organizational control operated effectively over a SOC 2 Type II observation period.

### Phase 5 — Tool-assisted assessment

Start with native AWS visibility and read-only checks where possible:

- AWS Console and resource configuration review.
- AWS IAM credential report and IAM Access Analyzer.
- AWS CloudTrail and CloudWatch.
- AWS Config, after checking recording and rule charges.
- AWS Security Hub, GuardDuty, and Inspector, only after reviewing current pricing, free-trial/credit eligibility, Region support, and activation impact.
- Prowler, ScoutSuite, Steampipe, or Checkov for suitable authorized checks; review permissions, tool versions, scan scope, and output sensitivity before running.
- Trivy for container image and filesystem checks when container workloads are in scope.

Tool output is evidence to investigate, not a final audit conclusion. Validate important findings manually and record false positives or accepted risks.

### Phase 6 — Findings, remediation, and retest

Each finding should include:
- Clear title and affected resource(s).
- Severity and rationale.
- Evidence and timestamp.
- Security/business impact.
- Reproduction or validation steps that are safe and authorized.
- Specific remediation guidance.
- Responsible owner and target date.
- Retest result and closure evidence.

Use a consistent risk model. Do not label every scanner alert Critical; consider exploitability, exposure, asset importance, compensating controls, and business impact.

Deliverable: prioritized findings register and remediation plan.

### Phase 7 — Reporting and evidence package

Produce:
- Executive summary.
- Scope, dates, authorization, assumptions, and exclusions.
- Architecture and asset inventory.
- Assessment methodology and baseline versions.
- Findings register with evidence references.
- Positive controls and areas not tested.
- Remediation roadmap and residual risks.
- Retest summary.
- Evidence index with secure storage locations and access restrictions.

Do not include secrets, access keys, passwords, private keys, raw sensitive customer data, or unnecessary personal data in the report or Git repository.

## Practical lab scenarios

1. **IAM review:** create a deliberately over-permissive lab policy, identify the risk, replace it with least privilege, and retest.
2. **Network exposure review:** identify an intentionally broad Security Group rule, trace the path, narrow access, and document before/after evidence.
3. **S3 data protection:** inspect public-access controls, bucket policy, encryption, and versioning; remediate an unsafe lab configuration.
4. **Audit logging:** verify CloudTrail coverage and log destination protections; create and validate a detection/use case.
5. **Vulnerability management:** scan a deliberately vulnerable container image or lab host, prioritize findings, remediate, and retest.
6. **Backup and recovery:** inspect backup coverage and perform a controlled restore test; record achieved recovery time and data point.
7. **Configuration baseline:** evaluate selected CIS AWS Foundations Benchmark recommendations and document applicability and exceptions.
8. **Mini cloud audit:** assess the lab end-to-end and produce a professional report with evidence and a prioritized remediation register.

Use intentionally vulnerable settings only in an isolated lab. Never weaken a production environment to create a demonstration.

## Cost and safety controls

- Prefer local/offline analysis and read-only AWS APIs where practical.
- Before enabling AWS Config, Security Hub, GuardDuty, Inspector, CloudTrail data events, or paid third-party tools, explain pricing and obtain explicit user approval.
- Avoid deploying NAT Gateway, Network Firewall, or multi-region resources solely for audit practice unless separately approved.
- Do not run high-volume scans or intrusive tests against production workloads without written authorization and a change window.
- Remove temporary resources and review ongoing charges after each exercise.
- Store evidence securely; keep only sanitized examples in the public GitHub repository.

## Boundaries: technical audit vs. formal attestation

This learning track prepares the learner for technical cloud security assessments, control reviews, remediation, and audit-readiness support.

It does not qualify the learner to:
- Issue a SOC 2 report or certification.
- Represent themselves as an independent SOC 2 auditor or CPA.
- Guarantee that a company will pass a SOC 2 examination.
- Claim that a short configuration review proves SOC 2 Type II operating effectiveness.

A qualified independent CPA firm performs the formal SOC 2 examination and issues the report. A technical consultant may support the organization by assessing infrastructure, improving controls, preparing technical evidence, and helping remediate gaps. The independent auditor must retain independence.

## Suggested references

- AWS Well-Architected Framework: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- AWS Security Pillar: https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html
- CIS Benchmarks: https://www.cisecurity.org/cis-benchmarks
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
- NIST SP 800-53: https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final
- ISO/IEC 27001 overview: https://www.iso.org/standard/27001
- AICPA SOC resources: https://www.aicpa-cima.com/resources/landing/system-and-organization-controls-soc-suite-of-services

## Completion criteria

The track is complete when the learner can independently:
- Define and document an authorized assessment scope.
- Inventory a small AWS environment and diagram its trust boundaries.
- Assess the core control domains above using native AWS evidence and at least one suitable assessment tool.
- Validate and prioritize findings.
- Recommend and demonstrate remediation in the lab.
- Retest controls and produce a clear technical cloud security assessment report.
- Explain the limits of the assessment and distinguish technical readiness support from formal SOC 2 attestation.
