# Assessment Context

## Purpose

This document defines the environment, evidence set and assumptions used in the segmentation assessment. It makes each scope decision and finding traceable to a stated condition.

## Environment

The project covers an omnichannel payment environment processing approximately 4.8 million card transactions per year. The e-commerce payment service runs in AWS while identity, administrative access and several operational services are shared across the wider enterprise.

The CISO sponsors the review. Cloud Infrastructure owns networking, Digital Commerce owns the payment application and Internal Audit challenges the final scope determination. A Qualified Security Assessor would make the formal assessment decision.

## Existing Scope Claim

Management claims that only three AWS payment subnets form the cardholder data environment. Their position is based on separate route tables, security groups and a firewall policy between payment workloads and the corporate network.

The claim excludes corporate identity, shared deployment tooling, central logging, shared backup services and administrator endpoints. The purpose of this project is to test whether those exclusions are defensible.

## Evidence Available

| Evidence ID | Item | Assessment use |
|---|---|---|
| EV-01 | Current AWS account and VPC diagram | Identifies declared payment boundaries |
| EV-02 | Transit gateway route export | Identifies reachable private networks |
| EV-03 | Firewall and security-group rule summary | Tests permitted flows |
| EV-04 | Cloud identity role and group export | Maps privileged access paths |
| EV-05 | CI/CD runner configuration and deployment role | Tests who can alter payment workloads |
| EV-06 | Sample payment application logs | Tests whether account data leaves the CDE |
| EV-07 | Backup vault policy and restore-role export | Tests access to payment snapshots |
| EV-08 | Previous penetration-test report dated 18 months ago | Tests currency of segmentation assurance |
| EV-09 | Change record for a transit gateway redesign | Determines whether retesting was triggered |

## Key Assumptions

1. Customers enter card details into an Orchid-hosted payment page.
2. The payment API receives primary account numbers before tokenization.
3. Full PAN is retained only in an encrypted settlement vault for a defined settlement process.
4. A debug logging field currently sends full PAN to a shared logging account.
5. A shared CI/CD runner can assume the production payment deployment role.
6. Corporate identity administrators can modify membership of the payment administrator group.
7. Payment database snapshots replicate to a shared backup account.
8. No current independent test proves that out-of-scope networks cannot reach the CDE.

## Evidence Boundaries

Evidence IDs define the records required to support the assessment. Finding ratings should be reviewed against current likelihood, exposure and business impact before use in another environment.

## Decision Constraint

The assessment may recommend inclusion in PCI DSS scope when a system stores, processes or transmits account data, connects to the CDE or can affect CDE security. Final validation of PCI DSS scope and compliance remains the responsibility of the assessed entity and its assessor.
