# Microsoft Ignite 2026 — master announcement inventory (working audit)

**Created:** 23 November 2026  
**Event:** 17–20 November 2026  
**Status:** INCOMPLETE — research inventory, NOT an exhaustive or publication-approved evidence register.

This inventory was assembled from the previously discussed scope and an initial direct check of Microsoft's [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/), [Sentinel announcement](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174), [Defender overview](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975), and [Entra overview](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) on 23 November. Other primary URLs are research leads from prior review, **not all revalidated in this pass**. An item here is an announced or suspected capability to reconcile; its presence does not establish release or tenant availability.

## Edition mapping

- **1:** AI & Agent Security
- **2:** Security Operations & Identity
- **3:** Azure Infrastructure & Cloud Security

## Inventory

| ID | Capability / distinct change to verify | Edition | Primary-source lead | Reported availability | Outstanding verification |
|---|---|---:|---|---|---|
| IGN-01 | ISOC opt-in, unified SIEM/XDR, retention and ingestion terms | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Mixed GA/preview | Verify eligibility and price conditions |
| IGN-02 | ISOC case management, playbooks, workbooks, UEBA, workspace creation | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | GA (as described) | Verify feature-by-feature scope |
| IGN-03 | ISOC SOC optimization, Content Hub, detections as code | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | Preview | Validate rollout |
| IGN-04 | Sentinel automation change audit logs | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Public preview | Portal visibility |
| IGN-05 | Sentinel 500+ connectors and new/expanded sources | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Mixed/unspecified | Map each connector release |
| IGN-06 | Sentinel 85+ Azure Functions connector modernization, CCF multi-instance | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Announced | Connector-level verification |
| IGN-07 | Sentinel CrowdStrike alert promotion, AWS/Okta attack disruption signals | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Announced | Validate product availability |
| IGN-08 | Sentinel UEBA/Behaviors for GuardDuty, Check Point, Zscaler, Fortinet | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Announced | Schema/tenant availability |
| IGN-09 | Sentinel ingest-time normalization and parser management | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Preview timing CONFLICT | Sentinel says December; Defender overview says now |
| IGN-10 | Sentinel Data & Connectors Overview health/latency monitoring | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | Preview (reported) | Check exact product documentation |
| IGN-11 | Sentinel Connector Builder Agent | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | GA target end of November (reported) | Future target, not proof GA |
| IGN-12 | Microsoft Perception platform and coordinated red/blue/green agents | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Mixed | Separate agent-level statuses |
| IGN-13 | Perception Triage Agent expansion | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Announced | 80% alert volume is not accuracy |
| IGN-14 | Perception Attack Investigation Agent | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Announced | Validate availability |
| IGN-15 | Perception Detection Authoring Agent | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Announced | Historical-data testing and governance |
| IGN-16 | Perception threat protection, risk reduction, web application pentest playbooks | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Mixed preview/GA | Per-capability status |
| IGN-17 | Perception API/MCP extensibility, approval and audit controls | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | Announced | Check access and licensing |
| IGN-18 | Defender vulnerability shielding and attack disruption | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/vulnerability-shielding-protect-the-time-before-the-patch/4572135) | Preview | Differentiate approval and autonomous controls |
| IGN-19 | Defender Threat Intelligence Agent and zero-day experience | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-security-blog/threat-intelligence-that-moves-at-the-speed-of-the-threat-what%E2%80%99s-new-at-microsof/4573823) | Mixed GA/preview | Check each release |
| IGN-20 | Defender ClickFix clipboard-command protection | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | Rolling out / target end 2026 (reported) | Check current endpoints |
| IGN-21 | Defender endpoint health dashboard | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | Public preview (reported) | Validate scope |
| IGN-22 | Defender deployment controls and offboarding keys | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | Announced; precise status uncertain | Release notes needed |
| IGN-23 | Defender shared mobile-device protections | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | Announced; precise status uncertain | Platform support |
| IGN-24 | Defender custom Linux file and Windows registry telemetry | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | Preview targeted Dec 9 (reported) | Not current release |
| IGN-25 | Teams QR URL protection and deepfake integrations | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | Mixed preview/provider-dependent | Check licensing |
| IGN-26 | Entra high assurance credentials and phishing-resistant onboarding | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Partner and tenant prerequisites |
| IGN-27 | Entra PIM JIT VM/Arc access, session review and least privilege | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Individual feature verification |
| IGN-28 | Entra PIM application/agent roles, PIM-only policy, bulk management | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Agent-specific details allocated E1 |
| IGN-29 | Entra Conditional Access policy plans | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/scale-access-controls-with-microsoft-entra-conditional-access-policy-plans/4569647) | Preview | Plan vs individual rule behavior |
| IGN-30 | Entra MemberOf Next and Transitive Reports To dynamic groups | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Migration caveats |
| IGN-31 | Entra guest lifecycle governance | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | GA | Verify tenant rollout |
| IGN-32 | Entra tenant governance and drift management | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Cross-tenant rights |
| IGN-33 | Entra identity hard-delete protection and Backup/Recovery Premium | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview | Retention and recovery limits |
| IGN-34 | Entra MCP Server for IT administrators | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | GA (reported) | Confirm API permissions |
| IGN-35 | Baseline Security Mode 2026 for Microsoft 365 | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft_365blog/ignite%E2%80%9926-spotlight-announcing-microsoft-baseline-security-mode-2026-general-ava/4572694) | GA phased rollout (reported) | 24 settings and tenant eligibility |
| IGN-36 | On-Premises Baseline Security Mode, EMS 2.0 and future milestones | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-security-blog/new-investments-to-reduce-on-premises-security-risk/4570381) | Planned | Original Nov 5 announcement; not new GA |
| IGN-37 | Intune software-compliance policies and vulnerability remediation agent | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftintuneblog/whats-new-in-microsoft-intune-at-microsoft-ignite-2026/4573839) | Preview (reported) | Check individual feature status |
| IGN-38 | Intune CIS/STIG auditing and software/device inventory | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftintuneblog/whats-new-in-microsoft-intune-at-microsoft-ignite-2026/4573839) | Preview (reported) | Validate details |
| IGN-39 | Intune application updates, shared device and Windows Server management | 2 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftintuneblog/whats-new-in-microsoft-intune-at-microsoft-ignite-2026/4573839) | Mixed previews | Separate admin use cases |
| IGN-40 | Edge for Business extension risk and protected-page restrictions | 2 | [Microsoft source](https://news.microsoft.com/events/ignite/2026/book-of-news/) | Mixed GA/preview | Book of News section-level check |
| IGN-41 | Windows Endpoint Security Platform and baseline protection | 2 | [Microsoft source](https://news.microsoft.com/events/ignite/2026/book-of-news/) | Mixed GA/private preview | Validate architecture |
| IGN-42 | Entra Agent ID lifecycle, agent-aware CA and Dynamic Agent Risk | 1 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Mixed | Edition 2 cross-reference only |
| IGN-43 | Defender local AI agent runtime security and third-party posture | 1 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | Mixed GA/preview | Edition 1 re-audit |
| IGN-44 | Purview agent DLP and agent data governance | 1 | [Microsoft source](https://news.microsoft.com/events/ignite/2026/book-of-news/) | Mixed | Needs deeper first-party audit |
| IGN-45 | Agent 365 governance, identity, evaluation and risk controls | 1 | [Microsoft source](https://news.microsoft.com/events/ignite/2026/book-of-news/) | Mixed | Needs deeper first-party audit |
| IGN-46 | Azure Firewall AI Security add-on, inspection and DLP | 3 | [Microsoft source](https://azure.microsoft.com/en-us/updates?id=580694) | Public preview (reported) | Verify functionality and dates |
| IGN-47 | Azure Agent Grid network/MCP controls | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-agent-grid/4573407) | Preview (reported) | Check eligible runtimes |
| IGN-48 | Azure AI Gateway management and Agent 365 integration | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/integrationsonazureblog/whats-new-in-azure-api-management-at-microsoft-ignite-2026/4574194) | GA (reported) | Verify supported policies |
| IGN-49 | Azure Front Door WAF AI bot ruleset | 3 | [Microsoft source](https://azure.microsoft.com/en-us/updates?id=581604) | Public preview (reported) | Default Log mode |
| IGN-50 | Azure Machine Configuration baseline remediation | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-introducing-security-baseline-remediation-in-machine-configuratio/4573899) | Public preview (reported) | Policy settings/locations |
| IGN-51 | Azure Artifact Validation VM image checks | 3 | [Microsoft source](https://azure.microsoft.com/en-us/updates?id=581249) | Public preview (reported) | Validate scan types |
| IGN-52 | Azure Infrastructure Resiliency Manager and Copilot integration | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-infrastructure-resiliency-manager-is-now-generally-available-with-ai-power/4573791) | GA (reported) | Check component details |
| IGN-53 | Azure Backup recovery and logically air-gapped vault changes | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-backup-logically-air-gapped-vault-and-cyber-recovery-readiness/4573796) | Mixed | Split by discrete release |
| IGN-54 | Azure confidential computing, enclaves and AKS confidential containers | 3 | [Microsoft source](https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-enterprise-ai-starts-with-the-infrastructure-beneath/4574943) | Mixed previews | Compare Book of News offerings |
| IGN-55 | Azure Chaos Studio Workspaces and AKS extension | 3 | [Microsoft source](https://news.microsoft.com/events/ignite/2026/book-of-news/) | GA | Newly identified; validate detailed release |
| IGN-56 | Edge agent-browsing controls and secure enterprise browser | 1 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Preview (reported) | Overlap with infrastructure networking |
| IGN-57 | Entra External ID customer authentication | 1 | [Microsoft source](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | Unverified inventory candidate | Needs source-specific extraction |

## Source register and collection limits

| Source family | Source | Coverage at creation |
|---|---|---|
| book | https://news.microsoft.com/events/ignite/2026/book-of-news/ | Opened directly; NOT comprehensively inventoried |
| sentinel | https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174 | Opened directly; NOT comprehensively inventoried |
| defender | https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975 | Opened directly; NOT comprehensively inventoried |
| endpoint | https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835 | Research lead; full article/section verification outstanding |
| entra | https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456 | Opened directly; NOT comprehensively inventoried |
| perception | https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834 | Research lead; full article/section verification outstanding |
| intel | https://techcommunity.microsoft.com/blog/microsoft-security-blog/threat-intelligence-that-moves-at-the-speed-of-the-threat-what%E2%80%99s-new-at-microsof/4573823 | Research lead; full article/section verification outstanding |
| shield | https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/vulnerability-shielding-protect-the-time-before-the-patch/4572135 | Research lead; full article/section verification outstanding |
| bsm | https://techcommunity.microsoft.com/blog/microsoft_365blog/ignite%E2%80%9926-spotlight-announcing-microsoft-baseline-security-mode-2026-general-ava/4572694 | Research lead; full article/section verification outstanding |
| onprem | https://techcommunity.microsoft.com/blog/microsoft-security-blog/new-investments-to-reduce-on-premises-security-risk/4570381 | Research lead; full article/section verification outstanding |
| intune | https://techcommunity.microsoft.com/blog/microsoftintuneblog/whats-new-in-microsoft-intune-at-microsoft-ignite-2026/4573839 | Research lead; full article/section verification outstanding |
| ca | https://techcommunity.microsoft.com/blog/microsoft-entra-blog/scale-access-controls-with-microsoft-entra-conditional-access-policy-plans/4569647 | Research lead; full article/section verification outstanding |
| fw | https://azure.microsoft.com/en-us/updates?id=580694 | Research lead; full article/section verification outstanding |
| grid | https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-agent-grid/4573407 | Research lead; full article/section verification outstanding |
| gateway | https://techcommunity.microsoft.com/blog/integrationsonazureblog/whats-new-in-azure-api-management-at-microsoft-ignite-2026/4574194 | Research lead; full article/section verification outstanding |
| waf | https://azure.microsoft.com/en-us/updates?id=581604 | Research lead; full article/section verification outstanding |
| machine | https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-introducing-security-baseline-remediation-in-machine-configuratio/4573899 | Research lead; full article/section verification outstanding |
| artifact | https://azure.microsoft.com/en-us/updates?id=581249 | Research lead; full article/section verification outstanding |
| resilience | https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-infrastructure-resiliency-manager-is-now-generally-available-with-ai-power/4573791 | Research lead; full article/section verification outstanding |
| backup | https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-backup-logically-air-gapped-vault-and-cyber-recovery-readiness/4573796 | Research lead; full article/section verification outstanding |
| compute | https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-enterprise-ai-starts-with-the-infrastructure-beneath/4574943 | Research lead; full article/section verification outstanding |

### Known conflicts and cautions

1. **Ingest-time normalization:** The November 17 [Sentinel post](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) states public preview is coming in December 2026; the [Defender overview](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) describes preview as currently available. Do not assert tenant availability without resolving the difference.
2. **Microsoft Perception:** Platform-level GA does not establish GA for every agent or playbook. The 80% figure is alert-volume coverage described by Microsoft, not measured triage accuracy.
3. **Dates:** Announcement publication, first preview/GA availability, subsequent rollout, and tenant validation must be separate fields in a final evidence register. The reported statuses in this initial Markdown table are placeholders pending source-level date reconciliation.
4. **On-premises BSM:** Its original November 5 announcement precedes Ignite. Future milestones are not present-day releases.
5. **No exhaustive coverage claim:** Intune, Purview, Windows, Edge, Agent 365, and Azure source families need full independent passes. Microsoft Learn histories, roadmap records, GitHub change logs, and links from each announcement need systematic review.
6. **No prior edition audit performed:** Existing published/draft Edition 1 text has not been retrieved or compared line-by-line. All entries need a disposition: accurately covered / partial / missing / inaccurate / duplicated / intentionally excluded.

### Definition of done

- Enumerate every relevant Book of News heading and first-party technical article; preserve the list of excluded headings and rationale.
- Independently search release notes/product announcements for each product family; record retrieval date, pagination and failures.
- Resolve duplicates to distinct features, preserve cross-edition assignments, and verify each technical claim against its exact article section.
- Capture exact original announcement date, revision date, feature release date and preview/GA/rollout status separately. Leave unknown values unknown.
- Reconcile all three drafts against this inventory and record coverage dispositions. Do not designate an edition publication-ready until unresolved material claims are cleared.

**Inventory row count: 57. This count is a research checklist total, not a count of verified announcements or released features.**
