# Executive Decision Memo

**To:** Chief Information Security Officer  
**From:** Francisco Fonseca, GRC Analyst  
**Subject:** PCI DSS segmentation scope-reduction decision  
**Scenario date:** 14 June 2026

## Decision Requested

Approve rejection of the current proposal to limit PCI DSS scope to Orchid Retail Group's three payment subnets. Authorize the 90-day remediation and evidence plan before the scope-reduction request is reconsidered.

## Why This Decision Is Necessary

The existing design separates payment workloads at subnet level, but it does not separate the services that can alter those workloads or receive their data. A shared deployment runner can change payment code. Corporate identity administrators can grant payment privileges. Full PAN is sent to central logging and payment snapshots are managed through a shared backup service.

These conditions mean the current documentation understates the assessment boundary. Accepting the narrower scope would reduce assessment effort on paper while leaving material trust relationships unexamined.

## Business Impact

Rejecting the scope reduction increases short-term assessment work and requires engineering effort. It also prevents the organization from defending a position that available evidence does not support. The remediation plan is designed to produce a smaller and more stable future boundary rather than repeatedly debating the same undocumented dependencies.

The highest-priority actions are to stop PAN leakage into logs and remove shared CI/CD deployment access. Those actions reduce direct exposure even if the wider scope decision takes longer.

## Required Actions

1. Stop PAN-bearing logging and control affected historical data.
2. Move payment deployments to dedicated infrastructure and privileges.
3. Separate payment administration from general corporate identity administration.
4. Isolate payment backups and restore privileges.
5. Replace broad internal routes with named approved dependencies.
6. Commission independent segmentation testing after remediation.
7. Refresh and approve the PCI DSS scope determination.

## Accountability

The CISO owns the scope decision. Engineering, Identity, Network Security, Resilience and the Payment Product Owner own remediation evidence. GRC coordinates evidence quality and records the final rationale. Internal Audit provides challenge. The assessor determines whether the resulting evidence supports the PCI DSS assessment position.

## Recommended Decision

**Reject the current scope-reduction claim and approve remediation.** Do not accept the risk of treating shared security-impacting systems as out of scope. Reconsider the decision only when critical and high findings are closed and an independent test confirms the revised boundary.
