# Microsoft Ignite 2026: What's Changing in Azure Infrastructure & Cloud Security?

*Azure networking, infrastructure protection, encryption, recovery, and controls for AI workloads.*

Microsoft Ignite 2026 included a number of changes to Azure infrastructure and cloud security, including new network controls for AI workloads, temporary protection for vulnerable Linux systems, expanded encryption and logging options, policy enforcement, and recovery capabilities.

Some of these features are generally available. Others remain in public or limited preview, and several confidential-computing capabilities are still in development. The release status matters when deciding what can be evaluated or deployed today.

This is the final edition of my Ignite coverage. [Part 1](https://adversarylab.substack.com/p/microsoft-ignite-2026-what-can-your) covered AI and agent security. Part 2 focused on Microsoft's integrated SOC, Defender, Sentinel, and identity. This edition looks at the infrastructure controls supporting those environments.

## Microsoft Ignite 2026: Azure Announcements at a Glance

- **Network security:** Azure Firewall AI inspection, Agent Grid, DDoS policy controls, network security perimeters, and improved flow-log attribution.
- **Infrastructure protection:** Azure Baseline Security Mode, Machine Configuration remediation, and Azure Adaptive Virtual Patching for supported Linux VMs.
- **Encryption and workload hardening:** Key Vault symmetric AES keys, Azure SQL TDE protectors, AKS Trusted Launch, and confidential VM disk protection.
- **Recovery and resilience:** Backup and restore previews, generally available Azure Infrastructure Resiliency Manager, and GA announcements for Chaos Studio workspaces and its AKS extension in the Book of News.
- **Cloud and AI infrastructure:** Azure AI Gateway, Azure Resource Manager MCP operations, and confidential-computing updates.

## Updates Worth a Closer Look

### 1. Azure Firewall and Network Security for AI

**Azure Firewall AI Security**

Microsoft announced five capabilities in an add-on to Azure Firewall Premium: inline AI anti-malware, inline AI application protection, prompt-injection protection, network data loss prevention, and AI-assisted policy analysis.

The malware capability uses specialized models to classify binary content without running a sandbox detonation. The application protection capability evaluates supported HTTP requests for exploit patterns, including SQL injection and path traversal.

For AI traffic, the firewall integrates with Azure AI Content Safety Prompt Shields to inspect supported *direct* prompt-injection attempts. Protection for indirect prompt injection is a future direction, not an announced current capability. Network DLP integrates with Microsoft Purview to evaluate supported outbound uploads and enforce a policy decision inline.

The AI policy feature evaluates configured firewall rules alongside observed traffic to suggest improvements and surface anomalies. These capabilities apply to traffic that traverses the supported inspection path; they do not automatically protect requests that bypass Azure Firewall.

The Azure Firewall Premium AI Security add-on is **in public preview**. Organizations should still verify supported traffic, specific configuration requirements, and regional or tenant eligibility before planning enforcement.

**Agent Grid**

Agent Grid is a separate network-security architecture for supported agent workloads. In public preview with limited supported runtimes, it places identity-based network and Layer 3–7 policies outside the agent's own execution environment.

Its announced capabilities include isolation, FQDN and URL filtering, MCP tool-level allow/block policies, TLS inspection, and integration with Prompt Shields. Microsoft describes workload identities using SPIFFE/SPIRE and mutually authenticated connectivity, along with communication flow maps and Azure Monitor/Log Analytics integration.

The preview supports ACI Agent Groups, AKS Agent Sandbox, and onboarded native Kubernetes workloads on AKS. An approved connection to an MCP server doesn't automatically mean every tool on that server should be permitted, which is one reason the tool-level policies are relevant.

Agent Grid and Azure Firewall address related but different enforcement points. Their supported workloads, deployment prerequisites, and policy scope should be reviewed separately.

**Sources:** [Azure Firewall public preview](https://azure.microsoft.com/en-us/updates?id=580694) | [Azure Firewall technical announcement](https://techcommunity.microsoft.com/blog/AzureNetworkingBlog/secure-ai-secure-with-ai-introducing-the-next-chapter-of-azure-firewall-/4573399) | [Agent Grid announcement](https://techcommunity.microsoft.com/blog/azurenetworkingblog/introducing-agent-grid/4573407) | [Azure Compute overview](https://techcommunity.microsoft.com/blog/azurecompute/ignite-2026-the-next-era-of-customer-ai-starts-with-the-infrastructure-beneath-i/4574943)

### 2. Azure Workload Protection, Baselines, and Governance

**Azure Baseline Security Mode**

Microsoft announced Azure Baseline Security Mode (Azure BSM) in public preview. Built on Azure Policy, the initial baseline contains seven controls across Azure Storage and Azure Key Vault.

For Storage, the controls address secure transfer, anonymous public access, minimum TLS version, and Shared Key authorization. For Key Vault, they address public network access, soft delete, and purge protection.

Azure BSM supports a central baseline assignment and compliance review, followed by enforcement as resource owners enroll eligible scopes. Organizations can review existing dependencies and exemptions before broad enforcement. This is particularly important where applications still depend on public endpoints or Shared Key authorization.

The dedicated Azure BSM announcement calls the feature **public preview**. A separate Microsoft 365 Baseline Security Mode post described Azure expansion as private preview, so organizations should confirm actual eligibility rather than treating the two statements as interchangeable.

**Machine Configuration security baseline remediation**

Azure Policy and Machine Configuration also introduced public-preview remediation for selected settings in supported Windows and Linux security baselines, Linux CIS benchmarks, and Linux STIG baselines.

Remediation is explicitly scoped. The assignment must use `DeployIfNotExists`, the individual setting must be marked `Remediate`, and target machine locations must be selected through `RemediationLocations`. Without these conditions, the applicable machines or settings remain in audit mode.

This allows organizations to audit broadly while applying configuration changes to selected workloads. Stopping remediation does not automatically undo settings already changed.


**Azure Adaptive Virtual Patching**

Azure Adaptive Virtual Patching is in **public preview**, initially for Azure Linux virtual machines and virtual machine scale sets. It combines vulnerability and workload context with an AI-directed Adaptive Shield to generate temporary controls. A workload extension helps collect telemetry and apply mitigations, which can include eBPF-based workload enforcement and network-level compensating controls.

This isn't a replacement for patch management. The underlying vulnerability remains until the software is fixed. The engineering questions are whether a proposed mitigation blocks the relevant exploit path, what benign application behavior it could affect, and how the control is removed or adjusted after patching.

**Azure Policy enforcement and inventory**

Azure Policy **Enrollments** is in public preview and supports a staged shift from evaluating compliance to enforcing policy on enrolled resources. Public-preview IP-filtering conditions allow supported deny decisions to consider the source IP address or CIDR range of a management request. This operates at the Azure Policy request-evaluation layer; it should not be described as a substitute for a network firewall.

Machine Inventory for Azure and Arc-enabled servers is also in public preview, providing collected inventory of supported software, services, accounts, and certificates. Microsoft's Configuration Manager connector for Azure Arc is a separate public preview that exposes Configuration Manager device inventory through Arc without changing its management authority.

**Sources:** [Azure BSM announcement](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/introducing-azure-baseline-security-mode-a-simpler-path-to-secure-by-default-azu/4573056) | [Machine Configuration announcement](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-introducing-security-baseline-remediation-in-machine-configuratio/4573899) | [Adaptive Virtual Patching](https://azure.microsoft.com/en-us/updates?id=580689) | [Azure governance roundup](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/azure-governance--management--microsoft-ignite-2026/4571751) | [Machine Inventory](https://techcommunity.microsoft.com/blog/azuregovernanceandmanagementblog/public-preview-see-whats-running-across-your-servers-with-machine-inventory/4573924) | [Configuration Manager connector](https://techcommunity.microsoft.com/blog/azurearcblog/announcing-the-configuration-manager-connector-for-azure-arc-preview/4569994)

### 3. Key Management and Database Encryption

**Azure Key Vault and Azure SQL encryption**

Azure Key Vault Premium now supports **generally available** symmetric `oct-HSM` AES keys for supported encryption, decryption, key wrapping, and unwrapping operations. The feature originally entered preview in July 2026 and moved to GA in November.

Azure SQL Database separately announced **GA support for AES-256 symmetric keys** stored in Azure Key Vault Premium or Azure Managed HSM as customer-managed Transparent Data Encryption (TDE) protectors. This provides another key-management option alongside RSA-based protectors. It is part of cryptographic agility planning, not evidence that a database is automatically resistant to every future quantum threat.

**Database access and recovery**

Azure DocumentDB's database- and collection-level custom RBAC is in **public preview**, allowing permissions to be scoped below the account level.

Azure HorizonDB is a GA service, but its security and recovery features have separate release statuses: customer-managed-key encryption at rest is **public preview**, while private-endpoint connectivity and geo-redundant backup/restore have distinct **GA** announcements.

For Azure Database for PostgreSQL, Microsoft's Ignite **Book of News reports immutable point-in-time backups as generally available**. Long-term snapshot-based backup v2 remains in preview.

Azure SQL Managed Instance also announced GA zone redundancy for supported next-generation General Purpose deployments and GA multi-database Managed Instance link, with separate regional and configuration requirements.

**Sources:** [Key Vault symmetric keys](https://azure.microsoft.com/en-us/updates?id=579374) | [Azure SQL AES-256 TDE](https://azure.microsoft.com/en-us/updates?id=579531) | [DocumentDB RBAC](https://azure.microsoft.com/en-us/updates?id=578262) | [HorizonDB CMK](https://azure.microsoft.com/en-us/updates?id=579540) | [HorizonDB private endpoints](https://azure.microsoft.com/en-us/updates?id=574153) | [HorizonDB backup](https://azure.microsoft.com/en-us/updates?id=574168) | [PostgreSQL announcement](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613) | [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) | [SQL MI announcement](https://techcommunity.microsoft.com/blog/azuresqlblog/azure-sql-managed-instance-gets-a-boost-new-capabilities-in-next-gen-general-pur/4573761)

### 4. Azure AI Gateway and Governed Cloud Operations

**Azure AI Gateway**

Azure AI Gateway is now generally available as a standalone managed service, following its public preview as an Azure API Management tier.

It provides centralized access and policies for supported models and MCP tools, including routing, authentication, content-safety controls, observability, token usage, quotas, and rate limits. Model Router remains in preview.

Microsoft also announced generally available Agent 365 integration with Azure API Management and Azure AI Gateway for supported tool discovery, access restrictions, and monitoring. Separately, the Unified Model API is GA for supported API Management v2 SKUs, and the Applications feature is in public preview for registering consuming applications with identity-based access.

**ARM MCP Server and Azure Copilot**

The Azure Resource Manager MCP Server is expanding from read access into creating and updating Azure resources. These actions continue to use the Azure management control plane, so applicable Azure Policy and permissions remain relevant.

Microsoft also announced GA for the Azure Copilot deployment agent, with Azure Copilot spaces and custom skills in public preview. Azure SRE Agent added public-preview governance capabilities including customer-managed keys, Entra Agent ID, and Agent 365 integration.

Azure Monitor health models are GA and provide application-level context linking resource health, dependencies, and business impact. This could be useful when an infrastructure issue spans multiple services, although effectiveness depends on how the workload and its dependencies are represented.

**Sources:** [Azure API Management and AI Gateway](https://techcommunity.microsoft.com/blog/integrationsonazureblog/whats-new-in-azure-api-management-at-microsoft-ignite-2026/4574194) | [Azure agentic operations](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/advancing-agentic-operations-on-azure-at-ignite-2026/4573831)

### 5. Backup, Recovery, and Resilience

**Azure Backup and cyber recovery**

Microsoft's Azure Backup announcements distinguish protecting recovery points from being able to restore them after a compromise.

The logically air-gapped vault approach uses logically isolated vaulted data with multi-user authorization; soft delete and encryption are default controls, while immutability requires appropriate configuration. Microsoft also described preview recovery features, including bulk Azure VM Safe Restore, cross-tenant restore, and Defender alert-based recovery-point threat detection. Those threat signals come from source VM alerts rather than a malware scan of stored backup data. A recovery point with no reported threats is not automatically confirmed clean.

Azure Backup **Region of Choice** is also in preview, supporting eligible choices of secondary recovery region. Recovery methods have workload, region, and configuration limits; availability for one workload does not establish support for all backups.

Azure Backup for Cosmos DB separately reached GA. Microsoft describes immutable vaulted recovery points with up to ten years of retention, daily incremental backups with a one-day RPO, cross-region restore, and additional account-scale support.

**Infrastructure resiliency and VM images**

Azure Infrastructure Resiliency Manager is now generally available, with zonal resiliency coverage expanded from 20 to 41 Azure services. A converged view brings infrastructure and backup posture closer together. The Resiliency Agent remains **in preview**, despite the core manager's GA status.

Microsoft's Ignite **Book of News reports general availability for Azure Chaos Studio Workspaces and the AKS extension**, supporting reusable resilience exercises for Azure workloads and Kubernetes applications.

Azure Compute Gallery soft delete also reached GA. It allows supported deleted image versions to be recovered during a configurable retention period, reducing the risk that an accidental deletion breaks image deployment workflows.

**Sources:** [Azure Backup security overview](https://learn.microsoft.com/en-us/azure/backup/security-overview) | [Region of Choice](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/beyond-availability-zones---building-resilience-across-regions-with-azure/4573795) | [Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) | [Chaos Studio product announcement](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/introducing-the-next-chapter-of-azure-chaos-studio/4574151) | [Backup and cyber recovery](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-backup-logically-air-gapped-vault-and-cyber-recovery-readiness/4573796) | [Azure Backup for Cosmos DB](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/strengthen-data-protection-with-azure-backup-for-azure-cosmos-db/4573659) | [Infrastructure Resiliency Manager](https://techcommunity.microsoft.com/blog/reliability-and-resiliency-in-azure/azure-infrastructure-resiliency-manager-is-now-generally-available-with-ai-power/4573791) | [Azure Compute Gallery soft delete](https://techcommunity.microsoft.com/blog/azurecompute/soft-delete-in-azure-compute-gallery-is-now-generally-available/4568500)

## Developments Worth Tracking

### Azure Bastion and DDoS Protection

Azure Bastion announced public-preview **RDP vision**, **SSH vision**, and **SSH command logs**. The first two provide AI-assisted summaries and noteworthy-activity insights for recorded privileged sessions; the third exposes SSH command details for review. These capabilities build on Azure Bastion Premium session recording rather than replacing the underlying recordings.

Azure DDoS Protection's **custom policies** reached GA. Administrators can set fixed packets-per-second mitigation thresholds for supported TCP, UDP, or TCP SYN traffic, rather than relying solely on automatically tuned thresholds for those protocols. Protection of supported **NAT Gateway StandardV2 public IPs** entered public preview; this protects the shared outbound IP without making the gateway accept unsolicited inbound connections.

Azure DDoS Protection added **peacetime telemetry** in public preview. Previously, supported DDoS packet metrics were populated during mitigation. Now protected public IPs can expose normal traffic metrics, including TCP, SYN, UDP, and other packet categories, so teams can establish baselines and test monitoring before an attack. The mitigation decision remains separate from these metrics.

**Sources:** [Azure Bastion](https://techcommunity.microsoft.com/blog/azurenetworkingblog/from-recordings-to-insights-azure-bastion-brings-ai-to-privileged-session-review/4573409) | [DDoS custom policies](https://azure.microsoft.com/en-us/updates?id=580852) | [DDoS NAT Gateway support](https://azure.microsoft.com/en-us/updates?id=580862) | [DDoS peacetime telemetry](https://techcommunity.microsoft.com/blog/azurenetworkingblog/announcing-public-preview-of-azure-ddos-protection-peacetime-telemetry/4574781)

### Network Watcher and Network Security Perimeter

Azure Network Watcher received several **public-preview** additions that improve traffic attribution. Virtual Network Flow Logs can include the `networkInterfaceIP` field, and Private Link Service flow logs add original client details, translated addresses, and connection identifiers. Packet capture insights add AI-assisted summaries and structured protocol-log options for supported captures.

The network security perimeter service also introduced public-preview **cross-perimeter links** and **inbound service-tag rules** for supported configurations. These are policy and telemetry changes with specific prerequisites, not a blanket ability to inspect all traffic across Azure.

**Sources:** [VNet Flow Logs interface context](https://azure.microsoft.com/en-us/updates?id=578787) | [Private Link flow log enrichment](https://azure.microsoft.com/en-us/updates?id=578792) | [Packet capture insights](https://azure.microsoft.com/en-us/updates?id=578172) | [Cross-perimeter links](https://azure.microsoft.com/en-us/updates?id=579206) | [Inbound service tags](https://azure.microsoft.com/en-us/updates?id=579201)

### Azure Front Door and AKS Network Policies

Azure Front Door Premium WAF introduced a public-preview AI bot ruleset. It distinguishes AI training crawlers, AI search crawlers, interactive agents, and miscellaneous or unverified AI bots. Each category begins in Log mode, allowing administrators to review activity before choosing enforcement actions.

Azure Firewall for Containers is also in public preview. It uses a Kubernetes controller and custom resources to translate pod- and namespace-scoped security policies into Azure Firewall configuration for supported AKS egress traffic. The preview has networking and deployment limitations, including no Azure CNI Overlay support and a requirement to route the relevant traffic through the firewall.

On AKS, **Windows Trusted Launch** entered public preview for supported Windows Server 2025 nodes, using Secure Boot and vTPM-backed measured boot. **OS disk encryption for supported confidential VM node pools** is also in preview, with Ubuntu 26.04 and confidential-VM-bound keys. Intel TDX confidential VM node support is GA with Azure Container Linux, while Ubuntu 26.04 support remains preview. Kubernetes Fleet Manager's security-patch auto-upgrade channel is GA for supported deployments.

**Sources:** [Front Door WAF ruleset](https://learn.microsoft.com/en-us/azure/web-application-firewall/afds/ai-bot-ruleset) | [Azure Firewall for Containers documentation](https://learn.microsoft.com/en-us/azure/firewall/deploy-firewall-for-containers) | [AKS Trusted Launch](https://azure.microsoft.com/en-us/updates?id=572591) | [AKS confidential OS disk encryption](https://azure.microsoft.com/en-us/updates?id=581125) | [AKS Intel TDX](https://azure.microsoft.com/en-us/updates?id=581130) | [AKS Ignite technical overview](https://techcommunity.microsoft.com/blog/appsonazureblog/run-models-and-agents-on-your-own-kubernetes-clusters-aks-at-microsoft-ignite-20/4573912)

### VM Image Validation and Windows Server Security

The public-preview `Microsoft.PlatformValidation` resource provider, announced in public preview under the names Azure Platform Validation / Azure Artifact Validation, allows teams to request VM-image validation before publishing or distributing an image. Supported checks include image format, boot/provisioning, OS quality, malware scanning, and vulnerability checks. Results report which tests passed, failed, or could not run.

For Windows Server 2028, Microsoft introduced Hardened Server Core in Insider Preview build 29706. New Server Core installations start with hundreds of hardened settings enabled, rather than requiring the organization to apply the same baseline after installation. This is **preview functionality for the next server release**, not a change to every current Windows Server deployment.

**Sources:** [Azure Platform Validation](https://techcommunity.microsoft.com/blog/azurecompute/public-preview-azure-artifact-validation-%E2%80%93-self-serve-validation-for-vm-images/4573178) | [Hardened Server Core](https://techcommunity.microsoft.com/blog/windowsservernewsandbestpractices/announcing-hardened-server-core-for-windows-server-insiders/4574239)

### Confidential Computing and Data Protection

Microsoft announced a gated preview of AMD EPYC Turin-based v7 confidential VMs, along with a technology showcase of confidential bare-metal AI workloads on NVIDIA Vera Rubin NVL72.

The broader confidential-computing update includes GA support for selected Intel TDX confidential AKS worker-node configurations and additional encryption and migration capabilities. The Ignite Book of News groups Azure Confidential Enclaves and AKS Kata CoCo confidential containers among the announced **previews**. More detailed confidential-computing posts describe some underlying enclave and child-VM designs as ongoing engineering, so support for particular SKUs and deployment paths should not be assumed.

Other relevant announcements include Azure Database for PostgreSQL confidential-compute options and confidential VMs on Azure Local supported by AMD SEV-SNP. Supported processors, regions, workloads, and attestation capabilities differ by product.

**Sources:** [Ignite Book of News](https://news.microsoft.com/events/ignite/2026/book-of-news/) | [Azure Confidential Computing Ignite overview](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/what%E2%80%99s-new-in-azure-confidential-computing-%E2%80%94-ignite-2026/4573909) | [Turin confidential VM preview](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/announcing-gated-preview-of-next-gen-azure-confidential-vms-with-5th-generation-/4570276) | [Future minimal-TCB work](https://techcommunity.microsoft.com/blog/AzureConfidentialComputingBlog/shrinking-the-trusted-computing-base-for-sensitive-cloud-workloads/4573926) | [PostgreSQL announcements](https://techcommunity.microsoft.com/blog/adforpostgresql/more-power-more-resilience-better-value-azure-database-for-postgresql-at-ignite-/4573613) | [Azure Local](https://techcommunity.microsoft.com/blog/azurearcblog/whats-new-with-sovereign-private-cloud-at-microsoft-ignite-2026/4573886)

## The Engineer's Assessment

Microsoft is trying to close security gaps at the infrastructure level by giving organizations more control and visibility over AI workloads. Solutions like Azure Firewall and Agent Grid give security teams more ways to inspect traffic, limit access, and monitor communications across supported workloads.

Even with these solutions in place, organizations still need to understand the systems they’re protecting and how the controls fit into the environment. Knowing that an agent connected to a service is a starting point. We also need to know what that service does, what data it handles, and how the agent is supposed to use it. We need to be able to trace the agent’s actions and network activity across those systems.

That context helps us understand whether the activity is expected in the environment.

## Closing

That wraps up the third and final part of my Microsoft Ignite 2026 coverage, focused on Azure infrastructure and cloud security.

As these capabilities become available, organizations should test them against their own infrastructure, dependencies, and operational requirements before broad deployment.

See you in the next one 👋
