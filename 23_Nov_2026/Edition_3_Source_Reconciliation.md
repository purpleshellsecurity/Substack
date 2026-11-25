# Edition 3 — Azure Infrastructure & Cloud Security source reconciliation

**Review date:** 24 November 2026  
**Report type:** First-party source-checked editorial inventory, NOT a claim of exhaustive Microsoft Ignite release enumeration or tenant testing.  
**Draft:** [Edition_3_Substack_Draft.md](./Edition_3_Substack_Draft.md)

This is the Edition 3 companion to the master inventory. It reconciles 32 originally assigned Edition 3 research rows plus independently discovered security updates. Sources were checked from public Microsoft blogs and Microsoft Learn, with Azure Updates IDs cross-checked through indexed search where the dynamic listing returned zero items.

## Main editorial coverage

| Subject | Original inventory IDs | Verified source and status | Disposition |
|---|---|---|---|
| Azure Firewall AI add-on | IGN-046 | [Azure Networking, Nov 17](https://techcommunity.microsoft.com/blog/AzureNetworkingBlog/secure-ai-secure-with-ai-introducing-the-next-chapter-of-azure-firewall-/4573399); five announced controls; per-feature preview eligibility not established | Closer look; explicitly avoid blanket GA |
| Agent Grid | IGN-047 | [Agent Grid, Nov 17](https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-agent-grid/4573407); limited preview corroborated by [Azure Compute](https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-customer-ai-starts-with-the-infrastructure-beneath-i/4574943) | Closer look; constrained runtimes |
| Azure AI Gateway / APIM | IGN-048 | [Azure API Management, Nov 17](https://techcommunity.microsoft.com/blog/integrationsonazureblog/whats-new-in-azure-api-management-at-microsoft-ignite-2026/4574194); standalone Gateway GA, Agent 365 gateway integration GA; router preview; APIM Applications preview | Closer look |
| Azure Front Door WAF bot ruleset | IGN-049 | [Microsoft Learn](https://learn.microsoft.com/en-us/azure/web-application-firewall/afds/ai-bot-ruleset); preview, all initial rules Log | Tracking |
| Machine Configuration remediation | IGN-050 | [Azure Governance, Nov 17](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-introducing-security-baseline-remediation-in-machine-configuratio/4573899); public preview with three opt-in conditions | Closer look |
| Azure image validation | IGN-051 | [Azure Compute, Nov 17](https://techcommunity.microsoft.com/blog/azurecompute/public-preview-azure-artifact-validation-%E2%80%93-self-serve-validation-for-vm-images/4573178); public preview for PlatformValidation | Tracking; correct initial product naming |
| Resiliency Manager | IGN-052 | [Resiliency, Nov 17](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-infrastructure-resiliency-manager-is-now-generally-available-with-ai-power/4573791); GA, 20 to 41 zonal services | Closer look |
| Backup and recovery | IGN-053,094,120–122 | [Cyber recovery, Nov 17](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-backup-logically-air-gapped-vault-and-cyber-recovery-readiness/4573796); [Cosmos DB GA, Nov 20](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/strengthen-data-protection-with-azure-backup-for-azure-cosmos-db/4573659); per workload availability not assumed | Closer look; no duplicate count |
| Confidential computing | IGN-054,069 | [Ignite confidential overview](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/what%E2%80%99s-new-in-azure-confidential-computing-%E2%80%94-ignite-2026/4573909); AMD v7 gated preview; future child/enclave/container work not current preview; various GA platform features | Tracking |
| Chaos Studio | IGN-055 | [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/); GA Workspaces and AKS extension | Resilience inventory, omitted from article for brevity; merits editorial consideration |
| Monitor health models | IGN-058 | [Azure operations](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/advancing-agentic-operations-on-azure-at-ignite-2026/4573831); GA | Closer look |
| Azure SRE Agent / ARM MCP / Copilot | IGN-059,060,118,119 | [Azure operations](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/advancing-agentic-operations-on-azure-at-ignite-2026/4573831); ARM MCP now create/update; Copilot deployment agent GA; spaces/skills preview; SRE new governance preview | Closer look |
| Agent sandbox on AKS | IGN-062 | [Compute](https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-customer-ai-starts-with-the-infrastructure-beneath-i/4574943); ACI sandbox public preview; Agent Grid preview distinct | Referenced; detailed isolation already in published Edition 1 |
| Windows Server | IGN-063 | [Hardened Server Core](https://techcommunity.microsoft.com/blog/windowsservernewsandbestpractices/announcing-hardened-server-core-for-windows-server-insiders/4574239); Insider preview build 29706 | Tracking |
| DocumentDB / HorizonDB / SQL MI | IGN-064–067,116 | [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/); separate unique-availability review not completed | **Not individually published as factual claims**; retain in research register |
| PostgreSQL recovery/compute | IGN-068–070 | [Postgres Ignite post](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613); separate feature statuses and processor restrictions | Tracking, not itemized release claim |
| Windows 365 redirection | IGN-086 | Already covered Edition 2 in published draft; overlap | Explicitly excluded from Edition 3 |
| Azure BSM | IGN-117,123 | [Azure Governance post](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/introducing-azure-baseline-security-mode-a-simpler-path-to-secure-by-default-azu/4573056) says public preview; M365 overview elsewhere says private preview | Closer look; conflict explicitly disclosed |

## Newly surfaced independently (not in original Edition 3 32-row selection)

| Product | Primary source | Status | Editorial disposition |
|---|---|---|---|
| Azure Bastion RDP vision, SSH vision and SSH command logs | [Nov 17 Azure Networking](https://techcommunity.microsoft.com/blog/azurenetworkingblog/from-recordings-to-insights-azure-bastion-brings-ai-to-privileged-session-review/4573409) | Public preview | Tracking |
| Azure DDoS peacetime telemetry | [Nov 19 Azure Networking](https://techcommunity.microsoft.com/blog/azurenetworkingblog/announcing-public-preview-of-azure-ddos-protection-peacetime-telemetry/4574781) | Public preview | Tracking; does not change mitigation |
| Azure Firewall for Containers AKS egress | [Microsoft Learn](https://learn.microsoft.com/en-us/azure/firewall/deploy-firewall-for-containers) | Public preview | Tracking; Kubernetes custom resources and required routing |
| Azure Compute Gallery soft delete | [Azure Compute, Nov 17](https://techcommunity.microsoft.com/blog/azurecompute/soft-delete-in-azure-compute-gallery-is-now-generally-available/4568500) | GA | Closer look |

## Important unresolved issues

1. **Azure Updates dynamic rendering:** [Azure Updates listing](https://azure.microsoft.com/en-us/updates/) returned 0 results for the queried IDs even though Microsoft's indexed announcement and Learn pages support the individual changes. This is a retrieval limitation, not evidence no features were announced.
2. **Azure BSM availability:** Dedicated Azure announcement says **public preview** and gives portal instructions; another Microsoft 365 BSM summary uses **private preview** for Azure. Do not flatten the conflict.
3. **Azure Firewall AI Security:** Dedicated technical post gives the five new capabilities but exact individual preview/GA and regional availability must be checked before promising deployment.
4. **Backups:** Cyber recovery post illustrates multiple restore pathways. Their support/availability is workload- and geography-specific; avoid asserting universal GA.
5. **Confidential computing:** Technology showcases and future engineering are not preview/GA products; the article preserves this.
6. **Database and hybrid security:** DocumentDB fine-grained RBAC, Azure SQL zone resiliency, and specific PostgreSQL immutable restore details were inventoried, but not each independently reconciled to specific release status. Not silently claimed available.
7. **No exhaustive release census:** Microsoft Learn dated logs, full Azure Updates pagination and tenant-specific Azure rollout were not completely audited. Editorial coverage of material security changes is stronger but not mathematically exhaustive.
8. **Assessment:** The Engineer's Assessment is a proposed direction, NOT the user's expressed personal position; review before publishing.

## Editorial source standard

The article links source material near each topic and distinguishes GA, public preview, limited preview, gated preview, future development, and unverified rollout. A cited Microsoft announcement proves a documented claim, not working configuration in a tenant.
