# Segmentation Control Assessment

## Assessment Objective

Determine whether technical and administrative controls isolate the proposed CDE from out-of-scope systems strongly enough to support a PCI DSS scope-reduction claim.

## Rating Method

Ratings reflect the simulated likelihood that a weakness could undermine the segmentation claim and the impact on account data or payment-system integrity.

| Rating | Meaning |
|---|---|
| Critical | Direct path to change CDE code or controls with insufficient isolation |
| High | Material data exposure or privileged control-plane weakness |
| Medium | Control assurance is incomplete or the boundary is broader than documented |
| Low | Limited effect with compensating controls and clear evidence |

## SEG-01: Shared CI/CD Runner Can Deploy To Payment Workloads

**Rating:** Critical  
**Status:** Open  
**Evidence basis:** EV-05

The shared runner used by non-payment teams can assume the production payment deployment role. A compromise of the runner or its build credentials could alter payment code, disable logging or capture PAN before tokenization.

The runner and its control path are security-impacting. Subnet separation does not reduce this risk because the trusted deployment relationship crosses the boundary by design.

**Required action:** Create a dedicated payment runner in a controlled account, require protected branches and signed artifacts, restrict the deployment role to the required resources and monitor every assumption of the role.

## SEG-02: Corporate Identity Can Influence Payment Privileges

**Rating:** High  
**Status:** Open  
**Evidence basis:** EV-04

Corporate identity administrators can change membership of the group mapped to payment administrator roles. The payment environment therefore depends on a wider administrative population than the scope statement acknowledges.

**Required action:** Establish separated privileged identities, approval-controlled group membership and phishing-resistant MFA. Limit the number of administrators who can alter the payment access path and review those changes through a dedicated alert.

## SEG-03: Full PAN Is Sent To Central Logging

**Rating:** High  
**Status:** Open  
**Evidence basis:** EV-06

A debug field in payment events contains full PAN. Events are forwarded to a shared logging account with a broad analyst audience. This creates an account-data store outside the declared CDE and directly invalidates the documented data flow.

**Required action:** Remove the field at source, add automated PAN detection to the log pipeline, restrict access to affected indexes and determine how historical data will be deleted or protected. Validate that application errors and retries do not reintroduce the field.

## SEG-04: Shared Backup Administration Expands Trust

**Rating:** High  
**Status:** Open  
**Evidence basis:** EV-07

Encrypted settlement snapshots replicate to a shared vault. Backup operators can assume a restore role without payment-owner approval. Encryption reduces disclosure risk but does not remove the backup service or its privileged control path from consideration.

**Required action:** Move payment snapshots to a dedicated vault, separate restore privileges from routine backup operations and require approved break-glass activation. Monitor restore attempts and test recovery without granting standing broad access.

## SEG-05: Payment Egress Is Broader Than Documented

**Rating:** Medium  
**Status:** Open  
**Evidence basis:** EV-02 and EV-03

The payment route table sends private destinations through a transit gateway. Firewall rules permit several broad internal ranges rather than named operational services. This makes the connected-system population difficult to prove and creates paths that are absent from the architecture diagram.

**Required action:** Replace broad ranges with documented service destinations and ports. Deny other private destinations, record business owners and verify the final rule set through positive and negative testing.

## SEG-06: Segmentation Was Not Retested After Routing Change

**Rating:** Medium  
**Status:** Open  
**Evidence basis:** EV-08 and EV-09

The last independent segmentation test is 18 months old. A transit gateway redesign occurred after that test and the change record contains no scope review or segmentation retest. The organization therefore lacks current evidence that the claimed boundary works as designed.

**Required action:** Complete an independent segmentation test after remediation. Add an annual test schedule and a change trigger for routes, firewall rules, identity paths, deployment mechanisms and data flows.

## Overall Conclusion

The segmentation design is not effective enough to support the proposed scope reduction. The most important failure is not a missing firewall rule. It is the combination of control-plane trust and undocumented account-data movement. The scope claim should remain rejected until critical and high findings are closed and the revised boundary passes independent testing.
