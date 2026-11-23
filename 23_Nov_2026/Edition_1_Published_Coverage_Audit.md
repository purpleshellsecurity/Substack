# Edition 1 — published article coverage audit

**Audited on:** 23 November 2026  
**Published article:** *Microsoft Ignite 2026: What Can Your AI Agents Actually Do?*  
**Published:** 22 November 2026  
**Substack post ID:** 226072339  
**Source for comparison:** User-supplied full Markdown export of the published post, 307 lines, received 23 November 2026. This audit compares the published text to the [working Ignite announcement inventory](./Ignite_2026_Announcement_Inventory.md), currently containing 124 research records. A match to the inventory is **not** independent validation of Microsoft's claims or GA status.

## Executive finding

The published article already covers the **main four control areas**: discovery/identity (lines 34–73); permissions, tools and network (75–135); runtime, Intune and AKS sandboxing (137–187); and Purview data protection/risk (189–245). Prior assessments that those subjects were broadly missing were **incorrect**. The article has genuine, narrower omissions, described below. Do not alter the published article on the basis of this audit alone.

## Coverage ledger

| Topic / related inventory IDs | Disposition in published article | Published lines | Outstanding substance |
|---|---|---:|---|
| Entra Agent ID across local and third-party agents (IGN-42, 98) | **Covered** | 48–56, 261–265 | Specific platform eligibility / identity-federation mechanics not covered |
| Local/third-party discovery and shadow/network discovery (IGN-42, 100, 115) | **Covered** | 42–48 | >60 types, Windows/macOS GA, shadow/network preview correctly distinguished in article |
| Lifecycle ownership, inactivity, remediation (IGN-42) | **Covered** | 58–68 | Action Center deferred to later section |
| Agent 365 secretless federation (IGN-98) | **Missing detail** | — | Third-party workload federation model not explained; confirm supported integration and status |
| Agent 365 guided connection wizard (IGN-99) | **Missing** | — | Product admin usability; may be an intentional low-priority omission |
| Agent 365 Tools Registry and plugin/skill governance (IGN-80, 81, 102) | **Covered** | 93–103, 261–267 | Registry GA versus external catalog private preview included |
| Agent 365 MCP gateways/tools and shadow MCP governance (IGN-81, 82, 115) | **Partial** | 99–103, 105–115 | Describes MCP visibility, dependency and network firewall; doesn't independently detail shadow MCP inventory and all governance workflows |
| Agent 365 multi-tenant governance (IGN-103) | **Missing** | — | Cross-tenant admin capability not described |
| Agent 365 Copilot Cowork administrative plugin (IGN-104) | **Missing** | — | AI-assisted admin with consequential-action approval not described |
| Agent 365 Action Center (IGN-78) | **Covered** | 269–273 | Planned December preview clearly distinguished |
| Agent 365 agent map/duplicate agents, centrally managed advanced plugins (IGN-79, 80) | **Partial** | 95–99 | Plugin/skill governance covered; Agent Map/duplication analysis absent |
| Agent 365 Export Agent Activity to Azure Monitor/Application Insights (IGN-101) | **Missing** | — | Concrete export/telemetry path absent |
| Agent 365 usage/FinOps insights (IGN-77, 83, 96) | **Missing** | — | Capacity/cost insights optional for security editorial, but explicit disposition required |
| Agent 365 third-party risk signal partners (IGN-84) | **Missing** | — | Check Point/Cyera/Darktrace/Zenity telemetry into Sentinel not described |
| Entra Conditional Access for assistive agents (IGN-42) | **Covered** | 81–91 | Distinction from employee and action-based control explained |
| Entra Global Secure Access/MCP firewall (IGN-42) | **Covered** | 105–115, 275–281 | Preview disclosure included |
| Agent Grid (IGN-47) | **Covered** | 117–129 | Scope and AKS/ACI supported environments included |
| Defender Windows local-agent runtime protection (IGN-43) | **Covered** | 143–155 | Claims need separate vendor/source verification, not a content omission |
| Defender third-party cloud-agent posture (IGN-43) | **Covered** | 151–155 | Preview status disclosed |
| Defender agent identity abuse / response (IGN-43) | **Covered** | 153–155 | Explicit Copilot CLI abuse and account/session actions |
| Intune software compliance and MXC (IGN-37, 90, 111) | **Covered for scoped agent controls** | 157–169 | SDK agent app protection (IGN-111) not separately covered |
| AKS sandbox, hosted Foundry agents (IGN-62) | **Covered** | 171–181 | Kata/ACI and separate Foundry preview covered |
| Purview auto-label scaling, adaptive scopes, classifier management (IGN-92, 108) | **Covered** | 195–205 | Quantified 100k→500k and 4m→20m present |
| Purview recurring classification and SIT improvements (IGN-105, 106) | **Covered** | 203–205, 251–259 | January timing present |
| Purview unlabeled Copilot DLP (IGN-91) | **Covered** | 207–215 | Future January preview accurately separated in text |
| Purview local agent DLP (IGN-93) | **Covered** | 217–227 | Conflicting preview scopes acknowledged |
| Agent 365 Dynamic Agent Risk/Purview signals (IGN-84, 110) | **Covered at umbrella level** | 229–239 | Specific Unified Agent Risk analytics / partner contributed signals not detailed |
| Foundry evaluation/production insights/optimizer (IGN-71, 72) | **Outside narrow governance focus; omitted** | — | Candidate for dedicated AI engineering follow-up, not demonstrably required in this issue |
| Windows 365 for Agents (IGN-88, 89), Copilot Code runtime (IGN-76) | **Not covered** | — | Alternative execution/identity platforms; scope overlap, deliberate editorial decision needed |
| GitHub code review/MDASH (IGN-73–75) | **Not covered** | — | AppSec/developer AI-security edge of scope; decide intentional exclusion |
| Defender/Purview broad SOC-only updates (IGN-02–25) | **Assigned Edition 2** | — | Not an Edition 1 omission by itself |
| Azure platform control-plane changes (IGN-46–70, 117–123) | **Assigned Edition 3** | — | Not an Edition 1 omission merely because related to agents |

## Most defensible follow-up additions

1. **Agent activity export:** Explicit description of Agent 365 activity/telemetry export to Azure Monitor/Application Insights (IGN-101), including supported logging content, privacy boundaries and availability after first-party verification.
2. **Identity federation:** Secretless workload identity federation for third-party agents (IGN-98), separate from the already covered existence of individual Agent IDs.
3. **Multi-tenant and MCP administration:** Multi-tenant management (IGN-103), shadow/unmanaged MCP-server inventory (IGN-82/115), and any distinct enforcement controls not already covered.
4. **Agent risk signals:** Specific partner telemetry and Unified Agent Risk functionality (IGN-84/110), if supported by primary source detail and in scope.
5. **Optional brief additions:** Agent Map/duplication review, connection wizard, Copilot Cowork governance, agent activity cost/usage, Intune application SDK protection, Windows 365 for Agents and Codename MDASH. These are worth recording, but not all warrant a correction to an already published article.

## Important corrections to earlier advice

- Previously claimed likely missing: **Agent 365 governance**. **Correction:** Tools Registry GA, managed plugins/skills, third-party MCP gateways and tool controls are explicitly present at lines 93–115. Only certain subfeatures are missing.
- Previously claimed likely missing: **Agent discovery and identity**. **Correction:** Device and network discovery, supported third-party platforms, Agent ID and lifecycle are well represented at lines 34–68.
- Previously claimed likely missing: **Purview DLP/classification**. **Correction:** Auto-label capacity, unified classification, Copilot unlabeled content, local-agent DLP and risk signals are explicitly present at lines 189–239.
- Previously claimed likely missing: **agent runtime/sandboxing**. **Correction:** Defender, Intune, MXC and AKS sandboxes are covered at lines 137–181.

## Unresolved verification

- **Content audit versus technical validation:** This is a comparison to the working research inventory, not an independent re-verification of every statement against Microsoft. Source-based status contradictions (e.g., Purview DLP preview coverage) remain flagged in the existing source audit.
- **No exhaustive source census yet:** Product release notes, roadmap/Message Center and all technical Ignite links have not been fully reconciled. Additional disclosures could emerge.
- **Do not claim published Edition 1 is missing broad categories** without pointing to an actual missing subfeature or incorrect claim.

**Publication disposition:** Edition 1 **already published**. Main control narrative is substantively represented. Suggested changes are optional follow-up/correction candidates pending source-by-source validation; no silent edit to the published article.
