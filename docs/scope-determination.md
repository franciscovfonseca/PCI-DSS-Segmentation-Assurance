# PCI DSS Scope Determination

## Decision

Orchid Retail Group cannot currently rely on network segmentation to limit PCI DSS scope to the three declared payment subnets. Shared services store account data, connect to payment systems or can affect the security of the CDE. They remain inside the assessment boundary until the identified dependencies are removed or controlled and the revised boundary is independently tested.

This determination is based on simulated evidence. It supports an assurance decision but does not establish PCI DSS compliance.

## Systems That Store, Process Or Transmit Account Data

| Component | Function | Account-data interaction | Scope decision |
|---|---|---|---|
| Cloud edge and WAF | Terminates and forwards payment sessions | Transmits payment requests | In scope |
| Commerce web tier | Hosts checkout workflow | Transmits PAN to payment API | In scope |
| Payment API | Authorizes and tokenizes transactions | Processes PAN | CDE |
| Managed key service | Performs cryptographic operations | Protects stored account data | In scope |
| Settlement vault | Retains encrypted settlement records | Stores encrypted PAN | CDE |
| Central logging account | Receives application events | Stores PAN because debug field is enabled | In scope |
| Shared backup account | Retains settlement snapshots | Stores copies of encrypted PAN | In scope |

The order platform receives a token and authorization result only. It is a candidate for exclusion after token behavior, error handling and support workflows are verified.

## Connected And Security-Impacting Systems

| System or service | Relationship | Security impact | Current decision |
|---|---|---|---|
| Corporate identity platform | Controls payment administrator group | Can grant privileged access | In scope as security-impacting |
| Shared cloud jump host | Provides administrative path | Can reach payment workloads | In scope |
| Shared CI/CD runner | Assumes production deployment role | Can change payment application code | In scope as security-impacting |
| Source repository and branch controls | Initiate production deployment | Can introduce unauthorized code | In scope as security-impacting |
| Transit gateway | Routes private network traffic | Can invalidate network isolation | In scope as security-impacting |
| Firewall management plane | Defines CDE access | Can alter the segmentation boundary | In scope as security-impacting |
| Backup restore role | Restores payment snapshots | Can expose or alter stored data | In scope as security-impacting |
| Central monitoring administrators | Access payment logs | Can view logged PAN | In scope while PAN remains in logs |

## Candidate Exclusions

| Environment | Proposed basis for exclusion | Evidence needed before approval |
|---|---|---|
| General corporate workstations | No permitted route to payment networks | Route analysis, firewall exports and negative connectivity tests |
| Human resources systems | No payment data or administrative trust | Data discovery result and dependency review |
| Marketing platform | Receives order analytics only | Field-level data-flow evidence and interface specification |
| Store guest Wi-Fi | Separate internet-only service | Network configuration and independent reachability test |
| Order platform | Receives token and result only | Tokenization design, log review and exception-flow testing |

These exclusions are not approved in the current state. Broad private-network egress and shared control-plane access prevent a clean conclusion.

## Scope Reduction Conditions

The organization may request reassessment when all of the following conditions are met:

1. Production payment deployments use a dedicated runner with a narrowly scoped role.
2. Payment administration uses separated privileged identities and dedicated administrator workstations.
3. PAN is removed from application logs and historical log data is handled under an approved remediation plan.
4. Payment backups use a dedicated vault, dedicated restore role and monitored break-glass process.
5. Network rules deny all undocumented private-network paths.
6. Architecture and data-flow diagrams match implemented routes and services.
7. An independent segmentation test confirms that out-of-scope networks cannot reach the CDE.
8. Scope is reconfirmed after the changes and approved by accountable stakeholders.

## Residual Risk

Even after technical isolation, scope can expand through future changes to deployment roles, logging fields, backup policies or routes. Orchid should treat scoping as a maintained control rather than a one-time diagram exercise. Change management must trigger scope review when systems, data flows or trust relationships change.
