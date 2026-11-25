# Edition 3 — Final coverage completeness cross-check (Microsoft Ignite 2026)

**Review date:** 24 November 2026  
**Source window:** 17–24 November 2026, with earlier publication dates retained for feature-history comparison.  
**Scope:** Edition 3 Azure Infrastructure & Cloud Security. This supplements [verified inventory](./Edition_3_Verified_Inventory.md).  
**Source constraint:** Azure Updates listing exposed **0 items in the noninteractive web response**. Individual Microsoft Azure Updates records **were retrievable via indexed search**. This is therefore a targeted cross-source audit, **not a full paginated export of Azure Updates**.

## Coverage conclusion

**Major finding:** The first reconciliation verified our *known* 32 entries but missed a meaningful set of Azure security updates. This pass found **20 additional candidates** from individual Azure Updates records. Several have high security relevance and should be incorporated before the article is published. Counts denote distinct feature *candidates*, not complete universe of product releases or deployed capabilities.

**Review outcome:** Cross-source editorial coverage audit performed and independently discovered candidates classified. **Full collection completeness remains unproven** because Azure Updates provided no enumeratable result count/page cursors through available retrieval. Do not label this as an exhaustive source census.

## Sources searched and retrieval evidence

| Source family | Method / accessible scope | Outcome | Limitation |
|---|---|---|---|
| [Ignite 2026 Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) | Opened full HTML document, reviewed Azure Brand/Infra, Core, Data and security-related intersections | Complete returned document (995 lines); original Azure sections reviewed | Event editorial selection is not every Azure update |
| [Azure Updates](https://azure.microsoft.com/en-us/updates/) | Opened listing; searched indexed site by date, category, product, exact feature and Azure Update IDs | Listing returned **0 Updates found**; independently retrieved **30 distinct indexed record IDs** and compared feature/status | No server-rendered pagination, no count denominator; cannot claim all November releases |
| [Azure Networking blog](https://techcommunity.microsoft.com/category/azure/blog/azurenetworkingblog/all-posts) | Reviewed all-posts index for Nov 17–24 and relevant primary technical posts | Found Adaptive Virtual Patching omitted by the first inventory | Blog index is a product-family subset |
| [Azure Governance blog](https://techcommunity.microsoft.com/category/azure/blog/azuregovernanceandmanagementblog) | Reviewed Nov 16–24 index, November 24 roundup and feature-specific posts | Earlier first reconciliation had captured BSM, Machine Inventory, Policy, ARM MCP | Some feed pages use dynamic content and partial index views |
| [Azure Compute blog](https://techcommunity.microsoft.com/category/azure/blog/azurecompute) | Checked Nov 17–24 headlines and security-sensitive announcements | AKS, confidential-VM and image-validation leads cross-checked | May omit product-specific Azure Updates |
| [Microsoft PostgreSQL announcement](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613) | Direct product source Nov 17; compared with Book of News | **Preview** for immutable PITR, contradicts Ignite Book of News **GA** | Release status unresolved across teams until newer specific release record or product team confirmation |
| [Azure Chaos Studio announcement](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/introducing-the-next-chapter-of-azure-chaos-studio/4574151) | Direct product source Nov 17; compared with Book of News | Workspaces **GA**, AKS extension **public preview** vs Book of News saying both GA | Documented conflict, do not silently choose overall GA |

## Individual Azure Updates release-record cross-check

| Azure Update ID | Capability | First-party reported status | Added | Disposition | Evidence note |
|---|---|---|---|---|---|
| [580689](https://azure.microsoft.com/en-us/updates?id=580689) | Azure Adaptive Virtual Patching | Public preview | 17 Nov | **NEW / HIGH** | Linux VMs/VMSS, eBPF and network compensating controls; temporary protection, not OS patching |
| [579374](https://azure.microsoft.com/en-us/updates?id=579374) | Key Vault Premium symmetric oct-HSM AES keys | GA | 17 Nov | **NEW / HIGH** | AES encryption/decryption/wrap/unwrap; July preview to Nov GA |
| [579531](https://azure.microsoft.com/en-us/updates?id=579531) | Azure SQL Database TDE protector using AES-256 symmetric keys | GA | 17 Nov | **NEW / HIGH** | AES-256 protectors in Key Vault Premium/Managed HSM |
| [579540](https://azure.microsoft.com/en-us/updates?id=579540) | HorizonDB CMK encryption at rest | Public preview | 17 Nov | **NEW / HIGH** | Do not conflate HorizonDB service GA with CMK preview |
| [574153](https://azure.microsoft.com/en-us/updates?id=574153) | HorizonDB private endpoint | GA | 17 Nov | **NEW / MEDIUM** | Separate newly GA network isolation capability |
| [574168](https://azure.microsoft.com/en-us/updates?id=574168) | HorizonDB geo-redundant backup and restore | GA | 17 Nov | **NEW / MEDIUM** | Cross-region recovery; distinct from Cosmos DB backup |
| [580852](https://azure.microsoft.com/en-us/updates?id=580852) | Azure DDoS custom policy thresholds | GA | 17 Nov | **NEW / HIGH** | Per-protocol fixed PPS thresholds and associations |
| [580862](https://azure.microsoft.com/en-us/updates?id=580862) | DDoS mitigation for NAT Gateway StandardV2 IP | Public preview | 17 Nov | **NEW / HIGH** | Protect outbound shared NAT public IP; not inbound service exposure |
| [579206](https://azure.microsoft.com/en-us/updates?id=579206) | Network security perimeter cross-perimeter link | Public preview | 17 Nov | **NEW / HIGH** | Secure connectivity across separately protected perimeters |
| [579201](https://azure.microsoft.com/en-us/updates?id=579201) | Network security perimeter inbound service tags | Public preview | 17 Nov | **NEW / MEDIUM** | Third-party service-tag source rules |
| [578797](https://azure.microsoft.com/en-us/updates?id=578797) | Network Watcher traffic-based NSG/security rule recommendations | Public preview | 17 Nov | **NEW / MEDIUM** | Recommendation review only; Azure Updates page has contradictory GA timeline label |
| [578792](https://azure.microsoft.com/en-us/updates?id=578792) | Network Watcher Private Link Service enriched flow logs | Public preview | 17 Nov | **NEW / HIGH** | Client source, translated address and connection ID context for VNet flow logs |
| [578787](https://azure.microsoft.com/en-us/updates?id=578787) | Network Watcher VNet Flow Logs networkInterfaceIP | Public preview | 17 Nov | **NEW / HIGH** | Capture interface IP context, resource attribution and investigation |
| [578172](https://azure.microsoft.com/en-us/updates?id=578172) | Network Watcher packet capture insights / protocol logs | Public preview | 17 Nov | **NEW / HIGH** | AI summary plus optional structured protocol logs in Log Analytics |
| [578602](https://azure.microsoft.com/en-us/updates?id=578602) | Network Watcher AI connection troubleshooting summary | Public preview | 17 Nov | **NEW / LOW** | Connectivity diagnosis rather than primarily security enforcement |
| [572591](https://azure.microsoft.com/en-us/updates?id=572591) | AKS Windows Trusted Launch nodes | Public preview | 17 Nov | **NEW / HIGH** | Windows Server 2025 Windows node pools; Secure Boot/vTPM |
| [581125](https://azure.microsoft.com/en-us/updates?id=581125) | AKS confidential VM node OS disk encryption | Public preview | 17 Nov | **NEW / HIGH** | Ubuntu 26.04 confidential VM pools; CVM-bound OS disk key |
| [580549](https://azure.microsoft.com/en-us/updates?id=580549) | Logic Apps Automation VNet integration | Public preview | 17 Nov | **NEW / MEDIUM** | Access private dependencies via customer VNet; overlap automation domain |
| [578980](https://azure.microsoft.com/en-us/updates?id=578980) | Functions Network Troubleshooter v2 managed identity check | Public preview | 17 Nov | **NEW / LOW** | Network dependency/managed identity diagnostics |
| [581180](https://azure.microsoft.com/en-us/updates?id=581180) | Azure Policy built-in for HorizonDB diagnostic settings | CONFLICT: metadata GA, description preview | 17 Nov | **NEW / MEDIUM** | Microsoft Azure Updates itself contradicts release status; no categorical status |
| [580684](https://azure.microsoft.com/en-us/updates?id=580684) | Agent Grid | Public preview | 17 Nov | **EXISTING / CONFLICT** | Azure Updates public preview; prior blog/inventory 'limited preview'—qualify eligibility |
| [580694](https://azure.microsoft.com/en-us/updates?id=580694) | Firewall Premium AI Security add-on | Public preview | 17 Nov | **EXISTING** | Already IGN-046 |
| [581604](https://azure.microsoft.com/en-us/updates?id=581604) | Front Door WAF AI bot ruleset | Public preview | 18 Nov | **EXISTING** | Already IGN-049 |
| [581963](https://azure.microsoft.com/en-us/updates?id=581963) | Azure Firewall for Containers | Public preview | 20 Nov | **EXISTING** | Already tracked in additions |
| [580699](https://azure.microsoft.com/en-us/updates?id=580699) | Azure Bastion vision | Public preview | 17 Nov | **EXISTING** | Already tracked |
| [581175](https://azure.microsoft.com/en-us/updates?id=581175) | DDoS peacetime telemetry | Public preview | 17 Nov | **EXISTING** | Already tracked |
| [579147](https://azure.microsoft.com/en-us/updates?id=579147) | Cosmos DB vaulted backup | GA | 17 Nov | **EXISTING** | Already in IGN-094 |
| [578044](https://azure.microsoft.com/en-us/updates?id=578044) | Cosmos DB vaulted backup alternate announcement record | GA | 17 Nov | **DUPLICATE** | Do not count as second release |
| [581160](https://azure.microsoft.com/en-us/updates?id=581160) | Ebsv6/Ebdsv6 Intel TME default | GA | 17 Nov | **CONTEXT** | Compute SKU launch; security feature not independently new |
| [580926](https://azure.microsoft.com/en-us/updates?id=580926) | ExpressRoute Direct link groups | Public preview | 17 Nov | **CONTEXT** | Networking resilience rather than specific security control |

*Evidence method:* Search-indexed excerpts from the Microsoft-owned Azure Updates record for each ID were checked. Due to the Azure Updates dynamic-rendering issue, opening several of these same URLs in a noninteractive fetch returned the empty listing rather than record text. This means the record titles, dates, and snippets were observed in search, not verified against a navigable paginated Azure Updates export.

## Important contradictions and corrections

1. **Chaos Studio AKS:** [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) says **Chaos Studio Workspaces and AKS extension GA**. [Dedicated Chaos Studio product announcement](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/introducing-the-next-chapter-of-azure-chaos-studio/4574151), Nov 17, says **Workspaces GA, AKS extension public preview**. Prior verified inventory already followed product post. Keep disagreement explicit; do not present extension as unqualified GA.
2. **PostgreSQL PITR immutability:** [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) says **GA**. [Product-team detailed article](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613) expressly says **Preview**. A [stable API release note](https://learn.microsoft.com/en-us/azure/postgresql/release-notes/release-notes-api) says GA API supports creating servers with immutable backups—but an API schema supporting the property does not settle service feature rollout status. Report **conflicting GA/preview statements**, using the preview description conservatively pending explicit product release confirmation; earlier file presented correction as fully settled, which was too strong.
3. **Agent Grid:** [Azure Updates 580684](https://azure.microsoft.com/en-us/updates?id=580684) calls **public preview**, while networking architecture article describes limited availability. Label public preview with limited eligible workloads/tenants as documented; do not imply universal access.
4. **HorizonDB Policy diagnostic setting:** [Azure Updates 581180](https://azure.microsoft.com/en-us/updates?id=581180) headline says Generally Available, but its own body states *available in preview*. Keep in conflict register, avoid categorical release claim.
5. **Network Watcher rule recommendations:** [Azure Updates 578797](https://azure.microsoft.com/en-us/updates?id=578797) heading/body public preview, but the status timeline metadata shows GENERAL AVAILABILITY. Use preview in editorial references while recording conflict.
6. **Azure BSM:** [Azure BSM-specific Nov 17 post](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/introducing-azure-baseline-security-mode-a-simpler-path-to-secure-by-default-azu/4573056) calls public preview; umbrella M365 BSM post called Azure private preview. Existing source reconciliation documents contradiction.

## Editorial decisions by priority

**Must add or materially expand before publishing**:

- **Azure Adaptive Virtual Patching (580689):** standalone major new security capability, public preview, initially Linux VMs and VMSS. Differentiate from Defender endpoint shielding in Edition 2.
- **Azure Key Vault symmetric keys (579374) + SQL TDE AES protector (579531):** GA, relevant cryptographic/key-protection changes. Avoid claiming quantum-proof security.
- **DDoS custom policies (580852) and NAT Gateway V2 coverage (580862):** GA vs public-preview separation; together with peacetime telemetry they form a meaningful network protection group.
- **Network Watcher Private Link flow logs (578792), interface attribution (578787), packet capture insights (578172):** public previews, directly relevant to investigation and logging.
- **HorizonDB CMK (579540), private endpoint (574153), recovery (574168):** split statuses; earlier umbrella service GA statement obscures preview feature scope.
- **Network security perimeter links (579206) and inbound service tags (579201):** two separate public-preview controls.
- **AKS Windows Trusted Launch (572591) and confidential OS disk encryption (581125):** two preview hardening features.

**Tracking/possible one-line treatment**:

- Network Watcher rule recommendation (578797), because status metadata conflicts; mention only after qualification.
- HorizonDB diagnostic settings policy (581180), ambiguous status; do not label GA.
- Logic Apps Automation VNet integration (580549) and Functions Network Troubleshooter v2 (578980); infrastructure integration but lower than direct protective controls.
- ExpressRoute link groups (580926) primarily network resiliency; less central.
- Ebsv6/Ebdsv6 TME (581160) is a compute launch, not a novel distinct security control.

**Already captured or duplicate:** Firewall add-on, Agent Grid, WAF bot ruleset, Firewall for Containers, Bastion vision, DDoS peacetime telemetry, Cosmos DB backup. Azure Updates 579147 and 578044 represent the same Cosmos backup release; avoid double counting.

## Editorial completion criterion

This document records the requested cross-source coverage check and the substantive omissions it detected. The important missed candidates now have individual first-party record IDs and disposition. The article draft **was not edited** during this review.

**Cannot honestly assert source completeness**: No pagination/count from Azure Updates and no reproducible machine-readable inventory dump was obtained, so no denominator against which to certify 100% collection. A fully exhaustive census requires a functioning Azure Updates query/export or Microsoft's Release Communications MCP API, then date-filter and compare full result IDs. **This is a separate collection-system limitation; it should not turn editorially qualified claims into fabricated GA statuses.**

**Next editorial step:** Merge selected high-priority additions into draft and do section-by-section claim-level verification; preserve Engineer's Assessment as user-review text.
