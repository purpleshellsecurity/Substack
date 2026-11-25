# Microsoft Ignite 2026: What's Changing in Azure Infrastructure & Cloud Security?

*Azure Firewall, Agent Grid, security baselines, recovery, and protection for AI workloads.*

Microsoft Ignite 2026 included a number of changes to Azure infrastructure and cloud security, including new network controls for AI workloads, expanded policy enforcement, image validation, and backup and recovery capabilities.

Some of these features are generally available. Others remain in public or limited preview, and several confidential-computing capabilities are still in development. The release status matters when deciding what can be evaluated or deployed today.

This is the final edition of my Ignite coverage. [Part 1](https://adversarylab.substack.com/p/microsoft-ignite-2026-what-can-your) covered AI and agent security. Part 2 focused on Microsoft's integrated SOC, Defender, Sentinel, and identity. This edition looks at the infrastructure controls supporting those environments.

## Microsoft Ignite 2026: Azure Announcements at a Glance

- **Azure networking:** New AI inspection capabilities for Azure Firewall, network-level agent controls with Agent Grid, and an AI bot ruleset for Azure Front Door WAF.
- **Azure governance:** Azure Baseline Security Mode and remediation for supported Machine Configuration baselines.
- **Infrastructure validation:** Azure Platform Validation for VM images, Azure Bastion privileged-session analysis, and AKS egress policies managed through Kubernetes resources.
- **Recovery and resilience:** New backup protections, clean recovery workflows, and generally available Azure Infrastructure Resiliency Manager.
- **Cloud and AI infrastructure:** Azure AI Gateway, governed ARM operations through MCP, and expanded confidential-computing options.

## Updates Worth a Closer Look

### 1. Azure Firewall and Network Security for AI

**Azure Firewall AI Security**

Microsoft announced five capabilities in an add-on to Azure Firewall Premium: inline AI anti-malware, inline AI application protection, prompt-injection protection, network data loss prevention, and AI-assisted policy analysis.

The malware capability uses specialized models to classify binary content without running a sandbox detonation. The application protection capability evaluates supported HTTP requests for exploit patterns, including SQL injection and path traversal.

For AI traffic, the firewall integrates with Azure AI Content Safety Prompt Shields to inspect supported *direct* prompt-injection attempts. Protection for indirect prompt injection is a future direction, not an announced current capability. Network DLP integrates with Microsoft Purview to evaluate supported outbound uploads and enforce a policy decision inline.

The AI policy feature evaluates configured firewall rules alongside observed traffic to suggest improvements and surface anomalies. These capabilities apply to traffic that traverses the supported inspection path; they do not automatically protect requests that bypass Azure Firewall.

Microsoft announced the add-on at Ignite. Organizations should verify individual capability availability, supported traffic, required configurations, and preview eligibility before planning production enforcement.

**Agent Grid**

Agent Grid is a separate network-security architecture for supported agent workloads. In limited preview, it places identity-based network and Layer 3–7 policies outside the agent's own execution environment.

Its announced capabilities include isolation, FQDN and URL filtering, MCP tool-level allow/block policies, TLS inspection, and integration with Prompt Shields. Microsoft describes workload identities using SPIFFE/SPIRE and mutually authenticated connectivity, along with communication flow maps and Azure Monitor/Log Analytics integration.

The preview supports ACI Agent Groups, AKS Agent Sandbox, and onboarded native Kubernetes workloads on AKS. An approved connection to an MCP server doesn't automatically mean every tool on that server should be permitted, which is one reason the tool-level policies are relevant.

Agent Grid and Azure Firewall address related but different enforcement points. Their supported workloads, deployment prerequisites, and policy scope should be reviewed separately.

**Sources:** [Azure Firewall announcement](https://techcommunity.microsoft.com/blog/AzureNetworkingBlog/secure-ai-secure-with-ai-introducing-the-next-chapter-of-azure-firewall-/4573399) | [Agent Grid announcement](https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-agent-grid/4573407) | [Azure Compute overview](https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-customer-ai-starts-with-the-infrastructure-beneath-i/4574943)

### 2. Azure Baseline Security Mode and Configuration Remediation

**Azure Baseline Security Mode**

Microsoft announced Azure Baseline Security Mode (Azure BSM) in public preview. Built on Azure Policy, the initial baseline contains seven controls across Azure Storage and Azure Key Vault.

For Storage, the controls address secure transfer, anonymous public access, minimum TLS version, and Shared Key authorization. For Key Vault, they address public network access, soft delete, and purge protection.

Azure BSM supports a central baseline assignment and compliance review, followed by enforcement as resource owners enroll eligible scopes. Organizations can review existing dependencies and exemptions before broad enforcement. This is particularly important where applications still depend on public endpoints or Shared Key authorization.

The dedicated Azure BSM announcement calls the feature **public preview**. A separate Microsoft 365 Baseline Security Mode post described Azure expansion as private preview, so organizations should confirm actual eligibility rather than treating the two statements as interchangeable.

**Machine Configuration security baseline remediation**

Azure Policy and Machine Configuration also introduced public-preview remediation for selected settings in supported Windows and Linux security baselines, Linux CIS benchmarks, and Linux STIG baselines.

Remediation is explicitly scoped. The assignment must use `DeployIfNotExists`, the individual setting must be marked `Remediate`, and target machine locations must be selected through `RemediationLocations`. Without these conditions, the applicable machines or settings remain in audit mode.

This allows organizations to audit broadly while applying configuration changes to selected workloads. Stopping remediation does not automatically undo settings already changed.

**Sources:** [Azure BSM announcement](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/introducing-azure-baseline-security-mode-a-simpler-path-to-secure-by-default-azu/4573056) | [Machine Configuration announcement](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-introducing-security-baseline-remediation-in-machine-configuratio/4573899)

### 3. Azure AI Gateway and Governed Cloud Operations

**Azure AI Gateway**

Azure AI Gateway is now generally available as a standalone managed service, following its public preview as an Azure API Management tier.

It provides centralized access and policies for supported models and MCP tools, including routing, authentication, content-safety controls, observability, token usage, quotas, and rate limits. Model Router remains in preview.

Microsoft also announced generally available Agent 365 integration with Azure API Management and Azure AI Gateway for supported tool discovery, access restrictions, and monitoring. Separately, the Unified Model API is GA for supported API Management v2 SKUs, and the Applications feature is in public preview for registering consuming applications with identity-based access.

**ARM MCP Server and Azure Copilot**

The Azure Resource Manager MCP Server is expanding from read access into creating and updating Azure resources. These actions continue to use the Azure management control plane, so applicable Azure Policy and permissions remain relevant.

Microsoft also announced GA for the Azure Copilot deployment agent, with Azure Copilot spaces and custom skills in public preview. Azure SRE Agent added public-preview governance capabilities including customer-managed keys, Entra Agent ID, and Agent 365 integration.

Azure Monitor health models are GA and provide application-level context linking resource health, dependencies, and business impact. This could be useful when an infrastructure issue spans multiple services, although effectiveness depends on how the workload and its dependencies are represented.

**Sources:** [Azure API Management and AI Gateway](https://techcommunity.microsoft.com/blog/integrationsonazureblog/whats-new-in-azure-api-management-at-microsoft-ignite-2026/4574194) | [Azure agentic operations](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/advancing-agentic-operations-on-azure-at-ignite-2026/4573831)

### 4. Backup, Recovery, and Resilience

**Azure Backup and cyber recovery**

Microsoft's Azure Backup announcements distinguish protecting recovery points from being able to restore them after a compromise.

Its logically air-gapped vault approach combines vaulted backup isolation with features such as locked immutability, always-on soft delete, multi-user authorization, and least-privilege access. Cyber recovery workflows described at Ignite include identifying potentially affected recovery points using Defender signals, cross-subscription or cross-tenant restore scenarios, and restoring multiple clean recovery points into an isolated environment.

These are related capabilities with distinct support and availability requirements. The announcement should not be taken to mean every recovery method is available for every workload and region.

Azure Backup for Cosmos DB separately reached GA. Microsoft describes immutable vaulted recovery points with up to ten years of retention, daily incremental backups with a one-day RPO, cross-region restore, and additional account-scale support.

**Infrastructure resiliency and VM images**

Azure Infrastructure Resiliency Manager is now generally available, with zonal resiliency coverage expanded from 20 to 41 Azure services. A converged view brings infrastructure and backup posture closer together, while the resiliency agent supports planning, dependency analysis, infrastructure-as-code review, and recovery exercises.

Azure Compute Gallery soft delete also reached GA. It allows supported deleted image versions to be recovered during a configurable retention period, reducing the risk that an accidental deletion breaks image deployment workflows.

**Sources:** [Backup and cyber recovery](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-backup-logically-air-gapped-vault-and-cyber-recovery-readiness/4573796) | [Azure Backup for Cosmos DB](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/strengthen-data-protection-with-azure-backup-for-azure-cosmos-db/4573659) | [Infrastructure Resiliency Manager](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-infrastructure-resiliency-manager-is-now-generally-available-with-ai-power/4573791) | [Azure Compute Gallery soft delete](https://techcommunity.microsoft.com/blog/azurecompute/soft-delete-in-azure-compute-gallery-is-now-generally-available/4568500)

## Developments Worth Tracking

### Azure Bastion and DDoS Protection

Azure Bastion announced public-preview **RDP vision**, **SSH vision**, and **SSH command logs**. The first two provide AI-assisted summaries and noteworthy-activity insights for recorded privileged sessions; the third exposes SSH command details for review. These capabilities build on Azure Bastion Premium session recording rather than replacing the underlying recordings.

Azure DDoS Protection added **peacetime telemetry** in public preview. Previously, supported DDoS packet metrics were populated during mitigation. Now protected public IPs can expose normal traffic metrics, including TCP, SYN, UDP, and other packet categories, so teams can establish baselines and test monitoring before an attack. The mitigation decision remains separate from these metrics.

**Sources:** [Azure Bastion](https://techcommunity.microsoft.com/blog/azurenetworkingblog/from-recordings-to-insights-azure-bastion-brings-ai-to-privileged-session-review/4573409) | [DDoS peacetime telemetry](https://techcommunity.microsoft.com/blog/azurenetworkingblog/announcing-public-preview-of-azure-ddos-protection-peacetime-telemetry/4574781)

### Azure Front Door and AKS Network Policies

Azure Front Door Premium WAF introduced a public-preview AI bot ruleset. It distinguishes AI training crawlers, AI search crawlers, interactive agents, and miscellaneous or unverified AI bots. Each category begins in Log mode, allowing administrators to review activity before choosing enforcement actions.

Azure Firewall for Containers is also in public preview. It uses a Kubernetes controller and custom resources to translate pod- and namespace-scoped security policies into Azure Firewall configuration for supported AKS egress traffic. The preview has networking and deployment limitations, including no Azure CNI Overlay support and a requirement to route the relevant traffic through the firewall.

**Sources:** [Front Door WAF ruleset](https://learn.microsoft.com/en-us/azure/web-application-firewall/afds/ai-bot-ruleset) | [Azure Firewall for Containers documentation](https://learn.microsoft.com/en-us/azure/firewall/deploy-firewall-for-containers)

### VM Image Validation and Windows Server Security

The new `Microsoft.PlatformValidation` resource provider, announced in public preview under the names Azure Platform Validation / Azure Artifact Validation, allows teams to request VM-image validation before publishing or distributing an image. Supported checks include image format, boot/provisioning, OS quality, malware scanning, and vulnerability checks. Results report which tests passed, failed, or could not run.

For Windows Server 2028, Microsoft introduced Hardened Server Core in Insider Preview build 29706. New Server Core installations start with hundreds of hardened settings enabled, rather than requiring the organization to apply the same baseline after installation. This is **preview functionality for the next server release**, not a change to every current Windows Server deployment.

**Sources:** [Azure Platform Validation](https://techcommunity.microsoft.com/blog/azurecompute/public-preview-azure-artifact-validation-%E2%80%93-self-serve-validation-for-vm-images/4573178) | [Hardened Server Core](https://techcommunity.microsoft.com/blog/windowsservernewsandbestpractices/announcing-hardened-server-core-for-windows-server-insiders/4574239)

### Confidential Computing and Data Protection

Microsoft announced a gated preview of AMD EPYC Turin-based v7 confidential VMs, along with a technology showcase of confidential bare-metal AI workloads on NVIDIA Vera Rubin NVL72.

The broader confidential-computing update includes GA support for selected Intel TDX confidential AKS worker-node configurations and additional encryption and migration capabilities. New confidential enclaves, Confidential Child Capable VMs, and next-generation confidential containers on AKS remain engineering work for future releases, not generally available Azure offerings.

Other relevant announcements include Azure Database for PostgreSQL flexible server recovery and confidential-compute options, and confidential VMs on Azure Local supported by AMD SEV-SNP. Supported processors, regions, workloads, and attestation capabilities differ by product.

**Sources:** [Azure Confidential Computing Ignite overview](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/what%E2%80%99s-new-in-azure-confidential-computing-%E2%80%94-ignite-2026/4573909) | [Turin confidential VM preview](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/announcing-gated-preview-of-next-gen-azure-confidential-vms-with-5th-generation-/4570276) | [Future minimal-TCB work](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/shrinking-the-trusted-computing-base-for-sensitive-cloud-workloads/4573926) | [PostgreSQL announcements](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613) | [Azure Local](https://techcommunity.microsoft.com/blog/azurearcblog/whats-new-with-sovereign-private-cloud-at-microsoft-ignite-2026/4573886)

## The Engineer's Assessment

*Proposed direction for editorial review, not yet your approved assessment.*

Across these announcements, Microsoft is adding more places to apply security controls directly in Azure infrastructure, from the network and identity layers to workload configuration, image validation, and recovery.

The part I would focus on is how those controls are applied in a real environment. A baseline that disables Shared Key access might improve security, but an application that still depends on it could stop working. An agent network policy can restrict connections, but only when the workload is supported and its traffic follows the intended enforcement path. A recovery policy is useful only if the organization has established that its critical applications can actually be restored.

That brings us back to business context. Organizations have different dependencies, acceptable downtime, and operational requirements. The engineering work is understanding those relationships and configuring the controls accordingly, then verifying they produce the expected result without disrupting the systems they're meant to protect.

## Closing

That wraps up the third and final part of my Microsoft Ignite 2026 coverage, focused on Azure infrastructure and cloud security.

As these capabilities become available, organizations should test them against their own infrastructure, dependencies, and operational requirements before broad deployment.

See you in the next one 👋
