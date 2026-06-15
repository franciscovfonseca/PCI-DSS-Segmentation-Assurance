# Auditor Challenge Pack

## Purpose

This pack prepares project owners to answer likely assessor questions with evidence rather than confidence statements.

## Challenge 1: Why Is The CDE Limited To Three Subnets?

**Current response:** It should not be limited to three subnets. The assessment found account-data flows and security-impacting services outside the declared boundary.

**Evidence required for a future response:** Current network diagram, current data-flow diagram, asset inventory, route exports, firewall exports and an approved scope rationale for every connected service.

**Failure condition:** The scope statement relies on network labels while shared services can deploy code, grant access or receive PAN.

## Challenge 2: Can Corporate Systems Reach The CDE?

**Current response:** The available route and firewall summaries do not support a complete negative assertion. Payment egress permits broad private ranges and the last segmentation test predates a transit routing change.

**Evidence required:** Representative negative tests from each excluded network, approved-flow tests, firewall events and an independent segmentation report.

**Failure condition:** Testing covers only one workstation or checks only inbound TCP connectivity.

## Challenge 3: Who Can Change Payment Workloads?

**Current response:** A shared CI/CD runner can assume the production deployment role. This makes the runner and its control path security-impacting.

**Evidence required:** Runner inventory, deployment-role policy, source-control permissions, protected-branch settings, artifact-signing evidence and deployment audit logs.

**Failure condition:** The organization lists only interactive administrators and ignores automated identities.

## Challenge 4: How Is Privileged Access Separated?

**Current response:** Corporate identity administrators can alter the payment administrator group. Current separation is insufficient for the proposed scope claim.

**Evidence required:** Privileged-group ownership, role mappings, approval records, MFA policy, administrator workstation controls and change alerts.

**Failure condition:** A dedicated payment role exists but a broad corporate group can change its membership.

## Challenge 5: Does Account Data Leave The Payment Network?

**Current response:** Yes. The reviewed log sample contains full PAN and is forwarded to a shared logging account. Encrypted settlement snapshots also replicate to a shared backup account.

**Evidence required:** Field-level data-flow mapping, log samples, PAN discovery results, backup inventory, encryption design and retention records.

**Failure condition:** The response assumes encryption or masking without testing normal and error paths.

## Challenge 6: When Was Segmentation Last Tested?

**Current response:** The previous test is 18 months old and predates a significant transit routing change. It cannot support a current effectiveness conclusion.

**Evidence required:** Independent report, tester independence record, source and target coverage, test results, remediation evidence and post-change retest records.

**Failure condition:** A vulnerability scan is presented as proof that out-of-scope networks cannot reach the CDE.

## Challenge 7: What Is Explicitly Out Of Scope?

**Current response:** Candidate exclusions have been identified but are not approved. Each exclusion has evidence conditions in the scope determination.

**Evidence required:** Data discovery, route evidence, interface specifications, negative tests and accountable approval.

**Failure condition:** The organization lists excluded systems without explaining how they are prevented from connecting to or affecting the CDE.

## Statements To Avoid

- "The firewall makes the environment compliant."
- "The data is encrypted, so the backup platform is out of scope."
- "The SIEM is a security tool, so it cannot be part of the CDE."
- "The diagram shows no connection."
- "We tested this last year."

## Defensible Closing Position

The correct current answer is that scope reduction has not been proven. Orchid has a defined remediation path and evidence plan, but the organization should keep the broader connected and security-impacting environment inside the assessment boundary until those actions are complete and independently tested.
