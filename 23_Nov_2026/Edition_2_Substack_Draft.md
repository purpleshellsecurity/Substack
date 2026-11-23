# Microsoft Ignite 2026: From Alerts to an Integrated SOC

*What's new across Microsoft Defender, Sentinel, Entra, Intune, and security automation.*

Microsoft Ignite 2026 brought several announcements across security operations and identity. Microsoft is expanding its integrated SOC experience, adding more security data and automation capabilities to Sentinel, and introducing new ways to protect endpoints and manage privileged access.

Some of these changes are generally available. Others are in preview or have rollout dates extending into December and 2027. I’ve kept those distinctions throughout.

This is the second of three Ignite editions. [The first edition](https://adversarylab.substack.com/p/microsoft-ignite-2026-what-can-your) covered AI and agent security, including discovery, identities, tool access and runtime protection. This edition focuses on day-to-day security operations, identity administration and endpoint protection. The final edition will cover Azure infrastructure and cloud security.

## Microsoft Ignite 2026: Security Announcements at a Glance

Here's the main picture from the Ignite announcements:

- **Microsoft Defender and Sentinel:** Expanded Integrated Security Operations Center (ISOC), with core capabilities generally available and additional SIEM functionality in preview.
- **Microsoft Sentinel:** Connector modernization, new telemetry sources, behavioral analytics, auditing for automation changes and tools for managing data ingestion.
- **Microsoft Perception:** Expanded triage, investigation, detection authoring, offensive validation and vulnerability-reduction workflows.
- **Defender endpoint protection:** ClickFix protection, endpoint health monitoring, deployment controls, shared mobile-device protection and additional telemetry collection.
- **Microsoft Entra:** New privileged access, Conditional Access, guest governance, authentication and identity recovery capabilities.
- **Intune and Microsoft 365:** Changes to vulnerability remediation, configuration auditing, application updates and Microsoft Baseline Security Mode 2026.

## Updates Worth a Closer Look

### 1. Integrated Security Operations Center

Microsoft announced expanded access to **Integrated Security Operations Center (ISOC)** within the Defender portal.

Core capabilities, including case management, playbooks, workbooks, UEBA, workspace creation and third-party data ingestion, are now generally available. Microsoft also expanded the preview to include the broader set of SIEM capabilities for eligible Defender customers.

Starting November 17, existing Sentinel customers with Microsoft 365 E5, Microsoft 365 E7 or Microsoft Defender Suite licenses can opt in to the experience. The Sentinel announcement describes 90 days of retention for eligible Defender data, up from 30 days, and an ingestion price of $2.40 per GB for qualifying customers. Those are conditional terms, not a universal change to every Sentinel workspace.

Microsoft also announced preview features including SOC optimization recommendations, Content Hub, detections as code and audit logs for automation changes.

The operational change is that SIEM data, Defender alerts, investigations and response workflows can increasingly be handled from a shared portal. For existing Sentinel environments, licensing eligibility and feature availability still need to be checked before planning a migration.

**Sources:** [Defender and Sentinel Ignite announcement](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | [Sentinel Ignite announcement](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174)

### 2. Microsoft Sentinel: Data, Detection and Automation

**Connector coverage and ingestion**

Microsoft says Sentinel now supports more than 500 connectors. That is the size of the overall connector catalog, not the number introduced at Ignite.

The Ignite announcements identify new or expanded integrations including Microsoft Edge for Business, Microsoft Copilot in government cloud environments, Microsoft Purview Information Protection, CrowdStrike API and RTEM, Wiz Push, Salesforce Audit Logs and OpenAI Audit Logs.

Microsoft also reports modernizing more than 85 Azure Functions-based connectors, expanding the Codeless Connector Framework (CCF), and adding multi-instance support so multiple source accounts can use separate credentials while sending data to the same workspace.

A separate connector announcement published November 11 showcases additional partner solutions such as Airlock Digital, BloodHound Enterprise and BlueVoyant Anthropic Claude Compliance. Those are relevant recent additions, but their appearance in the Ignite catalog should not be interpreted as proof that each connector first became available during the event.

**Cross-platform detections and behavioral analytics**

Sentinel can promote supported CrowdStrike detections into Defender alerts for correlation with other security signals. Microsoft also announced expanded AWS and Okta signals for identifying compromised identities and sessions and supporting additional attack-disruption scenarios.

Behavioral analytics expands to additional third-party sources: Fortinet behaviors, plus UEBA coverage for AWS GuardDuty, Check Point, Zscaler and Fortinet network data.

These changes matter when an investigation crosses endpoint, identity, SaaS and network boundaries. Teams still need to validate field mappings, correlation quality and which source activities are actually observable in their environments.

**Data operations and automation governance**

The public-preview Data & Connectors Overview brings connector health, ingestion volume and latency information into a unified management view. Related Unified Data Management capabilities, also in public preview, help administrators work with connectors, tables and ingestion health.

Also in public preview, Sentinel automation audit logs record the creation, modification, activation, deactivation and deletion of automation rules and generated playbooks. That creates an additional record for investigating unintended response-workflow changes.

The **Connector Builder Agent** uses AI-assisted development in Visual Studio Code to generate connector schemas, polling logic, UI and deployment assets, with validation capabilities. Microsoft targeted general availability for the end of November 2026. This was not a confirmed GA release at Ignite.

Finally, Microsoft announced **ingest-time normalization**, using Microsoft-managed parsers to standardize selected security logs as they are ingested. The dedicated Sentinel announcement says public preview is planned for December 2026. Microsoft's Defender overview describes the capability as already in preview, so the exact availability is inconsistent across those announcements. Because the two announcements give different preview timing, organizations should confirm availability in their environments before relying on the capability.

**Sources:** [Sentinel Ignite announcement](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ignite-2026-whats-new-in-microsoft-sentinel/4571174) | [Detailed connector announcement, November 11](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/microsoft-ignite-2026-new-sentinel-connectors-announcement/4565258) | [Defender and Sentinel overview](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975)

### 3. Microsoft Perception: Investigation, Detection and Exposure Reduction

Project Perception is now **Microsoft Perception**, with the platform announced as generally available. It coordinates specialized red, blue and green agents through playbooks for investigation, validation and remediation. That platform-level GA designation does not mean every individual agent or playbook is generally available.

**Triage and investigations**

Microsoft reports that Triage Agent coverage now extends to categories accounting for about 80% of the alert volume in its analysis of approximately eight million Defender alerts. That figure describes the portion of the analyzed alert population within the agent's coverage, not an independently measured accuracy rate or a guaranteed triage rate in every SOC.

The Attack Investigation Agent can reconstruct an incident timeline using evidence across endpoints, identities, email, Active Directory and cloud environments, including relevant activity that did not trigger an alert.

Microsoft is expanding third-party signals too. Its November 19 announcement describes Triage Agent support for selected Okta and Salesforce alerts, investigation using AWS and Okta data, and Detection Authoring Agent support for Okta, Salesforce and AWS. Support varies by agent rather than applying uniformly to every product.

**Detection authoring and threat intelligence**

The Detection Authoring Agent can use available tables, schemas and threat intelligence to produce tenant-aware KQL recommendations. The *Detect emerging threats* playbook can turn external threat research into proposed detection content, test it against historical tenant data to estimate alert volume, and surface tuning needs for analyst review before activation.

The Threat Intelligence Agent was also announced as generally available. It can structure information from external threat reports into behaviors, techniques and indicators that can be used in investigations and detection workflows.

**Offensive validation and risk reduction**

Perception's *Run web pen test* playbook uses an agent to test an authorized web application and produce findings with supporting evidence. The *Protect web app* playbook can use those findings to recommend mitigations, including changes to Azure Front Door WAF rules.

The *Reduce exposure risk* playbook works with the Risk Reduction Agent to prioritize exposed systems, coordinate supported patching through Intune or recommend temporary shielding while permanent remediation is pending.

Perception also supports APIs and MCP integrations so supported playbooks can be invoked from other SIEM, SOAR and ITSM workflows, with session artifacts returned for review. Usage dashboards and a cost calculator support operational management.

These are distinct workflows with different permissions, preview statuses and required human approvals. They should be evaluated individually.

**Sources:** [Perception Ignite announcement](https://techcommunity.microsoft.com/blog/perception-blog/whats-new-with-microsoft-perception-at-ignite-2026/4571834) | [Third-party signal expansion, November 19](https://techcommunity.microsoft.com/blog/perception-blog/more-signals-stronger-defense-microsoft-perception-expands-to-third-party-data/4573037) | [Threat intelligence announcement](https://techcommunity.microsoft.com/blog/microsoft-security-blog/threat-intelligence-that-moves-at-the-speed-of-the-threat-what%E2%80%99s-new-at-microsof/4573823)

### 4. Defender: Endpoint Protection and Vulnerability Shielding

**Protection against ClickFix**

Microsoft announced additional protection against ClickFix-style attacks, where a fake CAPTCHA or error message instructs someone to copy and execute a command. A component named `DefenderSessionHelper.exe` can examine copied commands and identify malicious clipboard content. The announced remediation clears the malicious content to interrupt the attack before execution.

Microsoft says the remediation was rolling out to Defender Antivirus devices, with completion targeted for the end of 2026. Customers with Defender can investigate the associated detections in the portal and advanced hunting.

**Endpoint operations and telemetry**

Microsoft also announced a consolidated endpoint health dashboard, with public preview rolling out over the following weeks. It brings together device inventory, sensor communication, antivirus service health, and update status. Other endpoint changes include staged deployment and preview controls for Defender updates, along with time-limited, traceable offboarding keys and packages.

Microsoft also announced support for shared Android and iOS devices configured with Entra shared-device mode and managed through Intune, so Defender protection remains associated with the device across different users.

Additional custom endpoint collection will cover selected Linux file operations and Windows registry key/value events. Public preview was targeted for **December 9, 2026**, so the capability should not be described as generally available at Ignite.

**Vulnerability shielding**

In public preview, Defender vulnerability shielding applies targeted temporary protections to vulnerable systems while patches are pending. The Risk Reduction Agent can recommend a protection plan for review; Defender attack disruption can apply certain targeted controls during an active attack.

Temporary shielding should be treated as an additional exposure-reduction control, not evidence that the underlying vulnerability has been remediated.

**Sources:** [Defender endpoint announcement](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-what%E2%80%99s-new-in-endpoint-security/4573835) | [Vulnerability shielding](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/vulnerability-shielding-protect-the-time-before-the-patch/4572135) | [Defender and Sentinel overview](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975)

### 5. Microsoft Entra: Authentication, Privileged Access and Governance

**Authentication and Conditional Access**

Microsoft announced preview *high-assurance credentials*, combining passkeys with trusted identity verification during enrollment, sensitive access and account recovery.

Conditional Access policy plans, also in preview, allow administrators to establish shared assignments, resources and conditions, then express access requirements as rules within the plan. This is relevant to organizations with large sets of overlapping policies. **Policy plans were originally announced November 4**, before Ignite, so their inclusion here is context for the Ignite identity discussion rather than a claim of a first release during the event.

**Privileged access**

Microsoft expanded preview Privileged Identity Management (PIM) capabilities, including just-in-time access to Azure and Azure Arc VMs, privileged session monitoring and recordings, and AI-assisted least-privilege recommendations. Additional planned or preview functions address application roles, AI agents, PIM-only role assignment policies and bulk management.

These features go beyond standard role activation. Session controls and recordings, in particular, change the evidence available for reviewing privileged activity.

**Group, guest and tenant governance**

New preview dynamic group features include **MemberOf Next**, combining membership from selected groups, and **Transitive Reports To**, extending membership through a reporting hierarchy.

Guest lifecycle governance was announced as generally available, allowing policies to account for sponsor information, invitation state and inactivity. Microsoft also announced preview cross-tenant configuration management and drift detection through Entra Tenant Governance.

**Identity recovery and administration**

Microsoft Entra Backup and Recovery Premium is in preview, with a 30-day retention offering and integration with Microsoft 365 Backup. Separate preview hard-deletion protection is intended to reduce the risk of permanently losing critical identity objects.

Microsoft also announced the **Microsoft MCP Server for IT Admins** as generally available, connecting supported AI tools with administration data and functionality across Entra, Purview and Intune.

**Sources:** [Microsoft Entra Ignite announcement](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/ai-is-changing-access-see-how-microsoft-entra-helps-you-stay-ahead-/4556456) | [Conditional Access policy plans, November 4](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/scale-access-controls-with-microsoft-entra-conditional-access-policy-plans/4569647)

## Developments Worth Tracking

### Microsoft Intune: Vulnerability Remediation and Configuration Auditing

The Intune Vulnerability Remediation Agent is in **limited public preview**. It combines Defender vulnerability intelligence and Intune device/application context to build remediation playbooks for prioritized exposure, including supported application and operating-system updates.

Intune Advanced Analytics adds **CIS benchmark auditing** in public preview during November, alongside existing DISA STIG auditing. These features report configuration compliance and individual checks; the audits themselves do not automatically change device settings.

Microsoft also announced private-preview Enterprise Application Management automatic updates and *app in-use detection*, which can identify running processes that block application installation and apply configured handling.

New and expanded inventory features include faster device and application reporting, registry/file inventory, and more explicit data freshness timestamps. Windows Server management through Intune is in Insider preview. Related Remote Help diagnostic and Autopilot device-preparation changes improve administrative visibility.

Intune's software compliance policy for unsanctioned agents was covered in Edition 1. It remains relevant here for endpoint administration, but I won't repeat that article's explanation.

**Source:** [Intune Ignite announcement](https://techcommunity.microsoft.com/blog/microsoftintuneblog/what%E2%80%99s-new-in-microsoft-intune-at-microsoft-ignite/4570003)

### Microsoft Baseline Security Mode 2026

Microsoft announced general availability of **Baseline Security Mode 2026** with a phased rollout across supported Microsoft 365 environments.

Compared with the 2025 baseline, this expands scope to Intune, Purview and Dynamics 365, introduces an Applications category, and adds **24 settings**. They include blocking non-allowlisted Office COM add-ins, requiring MFA for guests, requiring two administrators to approve sensitive Intune actions, preventing external guests from holding Purview eDiscovery roles and restricting overly broad application access to SharePoint and OneDrive data.

Administrators can examine individual settings and use simulation before enabling them. The Microsoft 365 version is GA with phased rollout. Azure and Windows baseline extensions will be covered separately in the infrastructure edition, where their preview availability can be distinguished by product.

**Source:** [Microsoft Baseline Security Mode 2026](https://techcommunity.microsoft.com/blog/microsoft_365blog/ignite%E2%80%9926-spotlight-announcing-microsoft-baseline-security-mode-2026-general-ava/4572694)

### Teams, Edge and Windows Protection

Defender's malicious-QR-code protection in Teams chats is in **public preview**. It can identify risky URLs embedded in QR codes, blur harmful material and present warnings, with supported investigation in advanced hunting. Microsoft's separate Teams meeting synthetic-audio/video detection relies on certified third-party providers; availability varies.

Microsoft also announced generally available extension safety information in Edge for Business, preview controls to restrict extensions from accessing protected pages, and a native Sentinel connector in preview for browser security telemetry. The capabilities have different licensing requirements: extension safety requires eligible Microsoft 365 licensing, extension leak controls require Microsoft 365 E3, and the Sentinel connector requires Sentinel licensing.

The **Windows Endpoint Security Platform** is available in supported Windows 11 releases. Its initial integration model is intended for approved security vendors, requiring Microsoft Virus Initiative enrollment and appropriate Artifact Signing. It should not be mistaken for a general-purpose API available to any process.

For remote desktops, **Windows 365 and Azure Virtual Desktop context-based redirection** is GA, allowing administrators to conditionally restrict clipboard, drive, printer and USB redirection according to Entra authentication context. Windows App Mobile Application Management for Windows remains in public preview.

**Sources:** [Defender and Teams announcements](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/ignite-2026-whats-new-in-microsoft-defender--sentinel/4569975) | [Edge for Business Ignite announcement](https://blogs.windows.com/msedgedev/2026/11/17/edge-for-business-ignite-2026-innovations/) | [Windows security What's New](https://learn.microsoft.com/en-us/windows/security/whats-new) | [Endpoint platform enrollment requirements](https://learn.microsoft.com/en-us/windows/win32/wesp/wesp-requirements) | [Windows 365 Ignite announcement](https://techcommunity.microsoft.com/blog/windows-itpro-blog/windows-365-at-ignite-2026-introducing-new-cloud-pc-capabilities-for-people-agen/4570006)

### On-Premises Baseline Security

Microsoft's on-premises baseline security initiative targets supported Exchange Server, SharePoint Server and Skype for Business Server deployments. It introduces work around automatic security update application, hardened configurations with drift detection and Emergency Mitigation Service 2.0.

The initiative was originally announced on **November 5**, before Ignite. The December 2026 and Q1 2027 dates are future milestones, not confirmation that the functionality was released during the conference.

**Source:** [New investments to reduce on-premises security risk](https://techcommunity.microsoft.com/blog/microsoft-security-blog/new-investments-to-reduce-on-premises-security-risk/4570381)

## What I'm Keeping an Eye On

The Sentinel connector and analytics changes are worth testing as they become available. Additional sources and normalization can help unify investigations, but a successful ingestion configuration still needs to be checked for field completeness, latency, schema mapping and detection behavior.

I'm also interested in Microsoft's agent-based detection authoring. Historical data checks and estimated alert volume are useful, but I would still want independent test cases to establish whether a detection identifies the intended behavior and how it handles benign activity.

The new Defender and Intune controls raise similar questions around deployment. A preview dashboard or policy may show an improved configuration state without confirming that the expected behavior is enforced on every supported endpoint.

## The Engineer's Assessment

Anyone who's worked in a SOC knows how much time goes into switching between tools, gathering evidence, and piecing together what happened during an incident.

During BRK324, Microsoft mentioned that SOC analysts work across an average of 10.9 different consoles during an incident. Having worked in security operations, I can attest that this is pretty accurate.

With ISOC, Microsoft is continuing its efforts to reduce the number of consoles analysts need to work across by integrating Sentinel, Defender, threat intelligence, exposure management, and response capabilities.

Bringing these capabilities together also creates an opportunity to provide security teams with insights that are more relevant to their business. Every organization has different systems, applications, dependencies, and risks. Understanding which assets support critical business functions, who owns them, and how they're connected helps determine which threats matter most and how organizations should respond.

Microsoft hasn't claimed to have completely solved this problem, but we're moving closer to centralized security capabilities that can use an organization's own data and business context to inform security decisions.

Now the real work begins: connecting these capabilities to the systems, data, and business processes they're meant to protect.

**Session reference:** [BRK324 — The Alert Is Dead: The Blueprint for the Agentic SOC](https://www.youtube.com/watch?v=Rz1Ky9Kf54I)

## Closing

That wraps up the second part of my Microsoft Ignite 2026 coverage, focused on security operations and identity.

The final edition will cover Azure infrastructure and cloud security.

See you in the next one 👋
