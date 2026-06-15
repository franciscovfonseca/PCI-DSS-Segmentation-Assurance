# Risk Register And Remediation Roadmap

## Treatment Principle

Remediation is sequenced by reduction of account-data exposure and control-plane trust, not by ease of implementation. The first actions stop PAN leakage and remove the broadest code-change path. Network cleanup follows because route restrictions cannot compensate for an unrestricted deployment role.

## Risk Register

| Risk ID | Risk statement | Rating | Owner | Treatment | Target |
|---|---|---:|---|---|---|
| R-01 | A compromised shared CI/CD runner could deploy malicious payment code and capture PAN | Critical | Director of Engineering | Mitigate | 30 days |
| R-02 | Corporate identity administrators could grant unauthorized payment privileges | High | Head of Identity | Mitigate | 60 days |
| R-03 | Full PAN in central logs could expose account data to a broad analyst population | High | Payment Product Owner | Mitigate | 7 days for new events, 45 days for historical data |
| R-04 | Shared backup privileges could permit unauthorized restore or disclosure of payment snapshots | High | Head of Resilience | Mitigate | 60 days |
| R-05 | Broad private egress could expose undocumented paths between the CDE and corporate services | Medium | Head of Network Security | Mitigate | 75 days |
| R-06 | Stale segmentation evidence could allow an ineffective boundary to remain unchallenged | Medium | GRC Lead | Mitigate | 90 days |

## First 7 Days

1. Disable the PAN-bearing debug field and validate normal, retry and error paths.
2. Restrict access to affected logging indexes and preserve investigation evidence.
3. Freeze changes that expand payment network routes or deployment-role trust.
4. Open tracked remediation items with named owners and decision authority.

## First 30 Days

1. Move production payment deployment to a dedicated runner and role.
2. Require protected branches, independent approval and signed build artifacts.
3. Inventory historical PAN in logs and approve deletion or protection actions.
4. Document every approved CDE flow with source, destination, port, protocol and owner.
5. Update architecture and data-flow diagrams from implemented configuration.

## Days 31 To 60

1. Introduce separated payment administrator identities and dedicated administrator workstations.
2. Restrict who can change the payment privileged group.
3. Create a dedicated payment backup vault and separated restore process.
4. Add alerts for deployment-role assumptions, privileged-group changes and snapshot restores.

## Days 61 To 90

1. Replace broad private-network rules with named dependencies.
2. Complete positive and negative path testing before production approval.
3. Commission an independent segmentation test.
4. Refresh the scope determination based on implemented evidence.
5. Present the revised decision to the CISO and Internal Audit.

## Decision Gates

| Gate | Required evidence | Decision owner |
|---|---|---|
| Stop PAN leakage | Clean log tests and historical-data treatment plan | Payment Product Owner |
| Remove shared deployment trust | Dedicated runner test and denied shared-runner attempt | Director of Engineering |
| Separate privileged administration | Identity export, approval workflow and access test | Head of Identity |
| Isolate backups | Vault policy, restore test and monitoring evidence | Head of Resilience |
| Approve segmentation design | Updated rules, diagrams and independent test | CISO with assessor input |

## Residual Risk Statement

After remediation, residual risk remains that future platform changes could reconnect shared services or reintroduce account data into logs. The proposed scope reduction should therefore be conditional on continuous route monitoring, privileged-change monitoring, data-loss detection and a formal change trigger for scope review.

Risk acceptance is not appropriate for R-01 or R-03 because both can directly affect payment integrity or expose account data. Any temporary acceptance of the remaining risks requires an expiry date, compensating controls and named executive approval.
