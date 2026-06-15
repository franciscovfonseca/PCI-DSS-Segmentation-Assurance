# Scenario And Assumptions

## Purpose

This document defines the simulated facts used in the assessment. It prevents an invented scenario from being presented as observed evidence and makes each judgment traceable to a stated condition.

## Organization

Orchid Retail Group is a fictional retailer with an e-commerce platform and 42 physical stores across the United Kingdom and Ireland. It processes approximately 4.8 million card transactions per year. The company is preparing for its next PCI DSS assessment and wants to reduce the number of systems presented to its assessor.

The Chief Information Security Officer sponsors the review. The Head of Infrastructure owns cloud networking. The Director of Digital Commerce owns the payment application. Internal Audit challenges the final scope determination. A Qualified Security Assessor would make the formal assessment decision.

## Existing Scope Claim

Management claims that only three AWS payment subnets form the cardholder data environment. Their position is based on separate route tables, security groups and a firewall policy between payment workloads and the corporate network.

The claim excludes corporate identity, shared deployment tooling, central logging, shared backup services and administrator endpoints. The purpose of this project is to test whether those exclusions are defensible.

## Simulated Evidence Available

| Evidence ID | Simulated item | Assessment use |
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

No live AWS exports, packet captures, identity records or payment data were used. Evidence IDs represent the records that should exist in a real review. Finding ratings reflect the simulated conditions and should not be reused without validating likelihood, exposure and business impact in the target environment.

## Decision Constraint

The assessment may recommend inclusion in PCI DSS scope when a system stores, processes or transmits account data, connects to the CDE or can affect CDE security. It may not declare Orchid Retail Group compliant. Final validation of PCI DSS scope and compliance remains the responsibility of the assessed entity and its assessor.
