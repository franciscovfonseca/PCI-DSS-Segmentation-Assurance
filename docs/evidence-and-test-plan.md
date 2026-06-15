# Evidence And Test Plan

## Objective

This plan defines the minimum evidence required to validate the current findings and support a future scope-reduction decision. It distinguishes document review from technical testing so that an architecture diagram cannot be treated as proof of effective segmentation.

## Evidence Collection Matrix

| Evidence | Owner | Collection method | Acceptance criteria |
|---|---|---|---|
| Current asset inventory | GRC and Cloud Operations | Export accounts, workloads, managed services and owners | Every component in the diagrams has an owner and scope rationale |
| Network and data-flow diagrams | Cloud Architecture | Review against implemented routes and interfaces | Diagrams show all CDE connections and account-data flows |
| Route and firewall configuration | Network Security | Export route tables, transit routes, security groups and firewall policies | No undocumented route or broad private destination remains |
| Identity configuration | Identity Security | Export privileged groups, role mappings and change logs | Only approved separated identities can grant or receive payment access |
| CI/CD configuration | DevSecOps | Export runner placement, role policy, branch controls and deployment logs | Shared runners cannot assume payment roles |
| Logging configuration | Application and SIEM owners | Review schemas, samples and detection results | No PAN is present in new events and affected historical data has a treatment record |
| Backup configuration | Resilience team | Export vault policy, role policy, key policy and restore logs | Payment restores require separated approval and dedicated access |
| Segmentation test report | Independent tester | Perform scoped positive and negative testing | Out-of-scope test points cannot reach CDE targets outside approved paths |

## Technical Test Cases

| Test ID | Test | Expected result | Evidence retained |
|---|---|---|---|
| NET-01 | Attempt CDE access from representative corporate subnets | Connection denied and logged | Source, destination, timestamp and firewall event |
| NET-02 | Test each approved management path | Only documented protocol, source and identity succeed | Session log and rule reference |
| NET-03 | Enumerate private routes from payment networks | Only approved dependencies are reachable | Route export and scan result |
| IAM-01 | Attempt payment-role assignment by standard identity administrator | Assignment denied | Audit event and policy result |
| IAM-02 | Review payment privileged-group changes | Every change has approval and alert evidence | Ticket and identity audit log |
| CICD-01 | Attempt payment deployment from shared runner | Role assumption denied | Runner log and cloud audit event |
| LOG-01 | Submit test account-data patterns through normal and error paths | PAN is blocked, masked or absent | Test event and detection output |
| BAK-01 | Attempt snapshot restore without payment approval | Restore denied and alerted | Vault event and alert record |
| CHG-01 | Simulate a routing change | Scope review and retest task are created | Change record and workflow evidence |

Test data must not contain live cardholder data. Approved synthetic values should be used and removed after testing.

## Segmentation Test Coverage

The independent test should use representative test points from each proposed out-of-scope network and target representative systems inside each CDE security zone. It should cover inbound paths, outbound paths and management paths. The tester should validate both network reachability and alternate trust paths through identity, deployment, logging and backup services.

Testing should be repeated after significant changes that could affect the boundary. At minimum, Orchid should treat routing, firewall, identity, CI/CD, logging, backup and payment data-flow changes as triggers for review.

## Evidence Quality Rules

1. Evidence must be generated from the implemented environment, not recreated manually for the assessment.
2. Screenshots require a source system, timestamp and accompanying export where possible.
3. Configuration exports must identify the account, region and collection time.
4. Test failures and exceptions remain in the evidence pack.
5. Every conclusion must point to an evidence ID and accountable owner.
6. Expired evidence cannot support a current control conclusion.

## Exit Criteria

The segmentation claim may return for approval only when all critical and high findings are closed, medium findings have approved treatment, evidence meets the acceptance criteria and an independent test confirms the intended isolation. GRC should then refresh the scope determination and record the approving authority.
