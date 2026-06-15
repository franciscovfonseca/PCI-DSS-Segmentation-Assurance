# Source Register

## Verification Record

Sources were reviewed on 14 June 2026. PCI Security Standards Council materials are treated as authoritative for PCI DSS requirements and guidance. The external GitHub portfolio was used only as inspiration for the project theme and decision-oriented learning objective.

## Primary Sources

| Source | Use in this project |
|---|---|
| [PCI Security Standards Council Document Library](https://www.pcisecuritystandards.org/document_library/) | Source of the current PCI DSS standard, supporting guidance and official assessment materials |
| [PCI DSS v4.0.1 publication announcement](https://blog.pcisecuritystandards.org/just-published-pci-dss-v4-0-1) | Confirms the limited revision and directs readers to the official document library |
| [PCI DSS Scoping and Segmentation Guidance for Modern Network Architectures](https://blog.pcisecuritystandards.org/new-information-supplement-pci-dss-scoping-and-segmentation-guidance-for-modern-network-architectures) | Informs the focus on modern control-plane dependencies, cloud architecture and defensible scoping |
| [PCI SSC FAQ 1576](https://www.pcisecuritystandards.org/faq/articles/Frequently_Asked_Question/What-does-adequate-segmented-environment-mean-when-determining-SAQ-eligibility/) | Supports the principle that segmentation must isolate systems and protect the CDE from out-of-scope compromise |
| [PCI DSS SAQ D for Merchants](https://listings.pcisecuritystandards.org/documents/PCI-DSS-v4-0-SAQ-D-Merchant.pdf) | Provides official testing language for diagrams, access restrictions, scope confirmation and segmentation testing |

## Inspiration Source

| Source | What was retained | What was changed |
|---|---|---|
| [Taimur Ijlal's GRC Projects overview](https://github.com/taimurijlal/GRCProjects) | Emphasis on judgment, defensible exclusions and audit challenge | Created a different company, architecture, evidence set, findings, deliverables and decision |
| [PCI DSS Network Segmentation project](https://github.com/taimurijlal/GRCProjects/tree/main/01-pci-dss-network-segmentation) | General topic of testing a segmentation claim | Replaced the original scenario with a hybrid cloud control-plane assessment and completed original artifacts |

## Claim Discipline

This project uses `assessed against`, `mapped to` and `supports` rather than claiming PCI DSS compliance. PCI DSS applicability depends on the real environment, implemented controls, evidence and assessor judgment. Readers should retrieve the current standard and guidance from PCI SSC before applying this work.
