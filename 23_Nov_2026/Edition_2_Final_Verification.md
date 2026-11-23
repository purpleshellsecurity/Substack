# Edition 2 — Final source verification and editorial disposition

**Date:** 23 November 2026  
**Companion:** [Edition_2_Verified_Inventory.md](./Edition_2_Verified_Inventory.md)  
**Draft:** [Edition_2_Substack_Draft.md](./Edition_2_Substack_Draft.md)

## Reviewed directly in this final pass

- [Defender & Sentinel Ignite overview](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) — source indexed and opened through Microsoft public page variant; confirms core ISOC GA vs expanded SIEM preview, Teams QR preview and provider-dependent synthetic media, vulnerability shielding preview.
- [Endpoint security deep dive](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) — search-indexed first-party content accessible; direct page fetch returned 403. Corroborated ClickFix rollout, shared mobile support, endpoint health, deployment/offboarding controls, future Linux/Windows event collection. **Full document direct retrieval remains a limitation.**
- [Entra Ignite overview](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) — indexed first-party full content accessible in search; direct page fetch returned 403. Confirms high-assurance credentials, CA plans, PIM, group governance, guest lifecycle, tenant governance, backup/recovery, MCP Server for IT Admins. **Full document direct retrieval remains a limitation.**
- [Sentinel Ignite post](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) — directly accessible; confirms opt-in licenses, $2.40/GB, 90-day eligible retention, connectors, behavioral analytics, auditing, Connector Builder GA target and normalization December preview target.
- [Sentinel connector catalog](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/microsoft-ignite-2026-new-sentinel-connectors-announcement/4565258) — directly accessible; original publication Nov 11. Named partner integrations and connector capabilities are *not* all new conference-day releases.
- [Perception Ignite overview](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) and [November 19 third-party expansion](https://techcommunity.microsoft.com/blog/perception-blog/more-signals-stronger-defense-microsoft-perception-expands-to-third-party-data/4573037) — confirm platform GA, distinct agent operations and third-party support (Triage: Okta/Salesforce; Investigation: AWS/Okta; Detection Authoring: AWS/Okta/Salesforce).
- [Threat intelligence Ignite post](https://techcommunity.microsoft.com/blog/microsoft-security-blog/threat-intelligence-that-moves-at-the-speed-of-the-threat-what%E2%80%99s-new-at-microsof/4573823) — zero-day/emerging-threat public preview and TI Agent GA.
- [Intune Ignite announcement](https://techcommunity.microsoft.com/blog/microsoftintuneblog/what%E2%80%99s-new-in-microsoft-intune-at-microsoft-ignite/4570003) — verified limited public, private, Insider, and public preview distinctions.
- [Microsoft 365 BSM 2026](https://techcommunity.microsoft.com/blog/microsoft_365blog/ignite%E2%80%9926-spotlight-announcing-microsoft-baseline-security-mode-2026-general-ava/4572694) — phased GA, 24 settings, Azure/Windows private preview.
- [Windows security release listing](https://learn.microsoft.com/en-us/windows/security/whats-new) and [Endpoint Security Platform requirements](https://learn.microsoft.com/en-us/windows/win32/wesp/wesp-requirements) — functionality and enrollment/signing restrictions for eligible security vendors.
- [Windows 365 Ignite post](https://techcommunity.microsoft.com/blog/windows-itpro-blog/windows-365-at-ignite-2026-introducing-new-cloud-pc-capabilities-for-people-agen/4570006) — context-based redirection GA; Windows App MAM public preview.
- [Conditional Access plans](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/scale-access-controls-with-microsoft-entra-conditional-access-policy-plans/4569647) and [on-premises security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/new-investments-to-reduce-on-premises-security-risk/4570381) — Nov 4 / Nov 5 **pre-Ignite** original publication dates.

## Source uncertainty and exclusions

- **Ingest-time normalization:** Sentinel says December 2026 preview, Defender umbrella says preview now. The article explicitly discloses this discrepancy and does not claim a tenant test.
- **Edge for Business:** Extension risk and protected-page controls are corroborated by the Ignite Book of News, but an independently opened product-specific technical release note was not verified. Draft has cautious language only.
- **Windows Endpoint Security Platform:** Initial support traces to October 2026 Windows 11 build prerequisites; Ignite promotion does not establish first launch during Nov 17–20.
- **Intune/Defender endpoint:** Some fine-grained feature rollouts remain unspecified. The article avoids assigning fabricated GA dates.
- **Microsoft 365 Message Center and tenant rollout:** Not accessed. No rollout/tenant installation claims are made.
- **GitHub detection-YAML releases:** Not exhaustively reconciled against all Ignite dates. The article does not claim a concrete number of newly released rules.
- **Microsoft Entra identity controls:** Some announced preview capabilities may have been discussed before Ignite; linked original posts are dated separately where known.
- **Azure infrastructure/security topics** assigned to Edition 3; **agent discovery, Agent ID, tool governance, agent runtime, Purview AI DLP** already treated in published Edition 1 and referenced rather than duplicated.

## Draft check against Edition 2 inventory

Each of the 49 Edition 2 research entries in the original inventory was given a disposition in the companion source ledger. The draft covers or combines ISOC, Sentinel operations/connector catalog, Perception, Defender threat intelligence and endpoints, Entra identity, Intune, BSM, Teams, Windows/Edge and on-premises security.

The following are condensed intentionally rather than silently omitted: detailed partner-by-partner Sentinel connector catalog (not all newly released), every exact BSM setting (link to first-party list), device-support tooling/Autopilot details (not principally security controls), Microsoft Perception MDASH/code scanning (more suitable for Edition 1 or separate AppSec research), and pre-Ignite CA/on-prem milestones (labeled context).

**Publication status:** Editorial draft ready for human review, **not** proof of exhaustive Microsoft release collection. Claim-level links are primary sources; any unresolved conflict is stated rather than hidden. No tenant-level validation performed.
