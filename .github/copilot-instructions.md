## Copilot instructions for NetApp Workload Factory for VMware documentation

### Repository overview
Product: NetApp Workload Factory for VMware

NetApp Workload Factory for VMware provides a planning center and migration advisors that help users analyze on-premises VMware VM configurations and migrate workloads to cloud environments, using cloud-native storage as external NFS datastores.

### Repository structure

All content files reside at the repository root. There are no subdirectories for topic areas.

- `learn-about-vmware-workloads.adoc` – Product overview: concepts, capabilities, supported targets, and licensing
- `quick-start-evs.adoc` – Quick start for migrating to Amazon Elastic VMware Service (EVS)
- `quick-start-native.adoc` – Quick start for migrating to Amazon EC2
- `quick-start.adoc` – Quick start for migrating to VMware Cloud on AWS
- `quick-start-gcve.adoc` – Quick start for migrating to Google Cloud VMware Engine
- `explore-planning-center.adoc` – How to manage VM inventory datasets and migration plans in the planning center
- `upload-vm-inventory.adoc` – How to collect and upload VM inventory data using RVTools, the data collector script, or Data Infrastructure Insights
- `launch-migration-advisor-evs.adoc` – Create a deployment plan for Amazon EVS using the migration advisor
- `launch-migration-advisor-evs-manual.adoc` – Manually create a deployment plan for Amazon EVS
- `launch-migration-advisor-gcve.adoc` – Create a deployment plan for Google Cloud VMware Engine
- `launch-onboarding-advisor.adoc` – Create a deployment plan for VMware Cloud on AWS
- `launch-onboarding-advisor-native.adoc` – Create a deployment plan for Amazon EC2
- `deploy-fsx-file-system-evs.adoc` – Deploy the FSx for ONTAP file system for Amazon EVS
- `deploy-fsx-file-system-native.adoc` – Deploy the FSx for ONTAP file system for Amazon EC2
- `deploy-fsx-file-system.adoc` – Deploy the FSx for ONTAP file system for VMware Cloud on AWS
- `connect-sddc-to-fsx.adoc` – Connect FSx for ONTAP to VMware Cloud on AWS
- `migrate-data.adoc` – Migrate VM data to the new VMware Cloud on AWS infrastructure
- `configuration-analysis.adoc` – Overview of EVS configuration analysis and well-architected best practices
- `view-evs-well-architected.adoc` – Review and remediate well-architected findings for EVS environments
- `calculate-evs-savings.adoc` – Explore cost savings for Amazon EVS
- `capture-vm-configurations.adoc` – Capture VM configurations for VMware Cloud on AWS (unpublished)
- `capture-vm-configurations-native.adoc` – Capture VM configurations for Amazon EC2 (unpublished)
- `whats-new.adoc` – Release notes landing page that includes content from `_whatsnew/`
- `_whatsnew/` – AsciiDoc include files for individual release note entries
- `media/` – Images used in the documentation
- `project.yml` – Site-level configuration: navigation sidebar, PDF settings, RSS page
- `_index.yml` – Landing page configuration

### Product-specific context

**Architecture and components:**
- *VMware planning center* – The main dashboard in Workload Factory for VMware; users upload VM inventory and manage migration plans here
- *Migration advisors* – Wizard-driven tools within the planning center; one advisor exists for each migration target (EVS, EC2, VMware Cloud on AWS, GCVE)
- *Amazon FSx for NetApp ONTAP* (FSx for ONTAP) – External NFS datastore used for AWS migration targets (EVS, EC2, VMware Cloud on AWS); deployed as part of the migration workflow
- *Google Cloud NetApp Volumes* – External NFS datastore used for Google Cloud VMware Engine environments
- *Well-architected analysis* – Automated daily scan of discovered EVS environments using AWS APIs; identifies configuration issues across reliability and security pillars; does not require vSphere credentials
- *Codebox* – In-product panel that surfaces CloudFormation templates and scripts for users operating in read-only or Basic mode

**Key concepts:**
- *VM inventory dataset* – A saved collection of VM configuration data uploaded from RVTools, the data collector script, or NetApp Data Infrastructure Insights; stored in the planning center for reuse
- *Deployment plan / migration plan* – The output of a migration advisor run; defines which VMs to migrate and the recommended FSx for ONTAP or Google Cloud NetApp Volumes configuration; can be saved, edited, provisioned, or exported as PDF/CSV
- *External datastore* – An NFS datastore provided by FSx for ONTAP or Google Cloud NetApp Volumes that supplements or replaces vSAN storage; scales independently of compute
- *Data collector script* (`list-vms.ps1`) – A PowerShell script distributed through the migration advisor Codebox; collects current VM performance data (IOPS, throughput) from vCenter using PowerCLI
- *RVTools* – A third-party Windows application that exports VMware environment data to an xlsx file; used for quick assessments when performance statistics are not needed
- *NetApp Data Infrastructure Insights* – A cloud infrastructure monitoring tool that can supply VM inventory data to the planning advisor via API
- *Well-architected pillars* – The EVS analysis currently covers *reliability* (partition placement group distribution) and *security* (EC2 stop and termination protection for ESXi nodes)

**Naming conventions and terminology:**
- The product is *NetApp Workload Factory for VMware*, commonly shortened to *Workload Factory for VMware* or just *Workload Factory* in context
- Migration target abbreviations: *EVS* = Amazon Elastic VMware Service; *VMC* = VMware Cloud on AWS; *EC2* = Amazon EC2; *GCVE* = Google Cloud VMware Engine
- *FSx for ONTAP* is the standard short form for Amazon FSx for NetApp ONTAP; avoid "FSx for NetApp" alone
- *SDDC* refers to a software-defined data center, specifically the VMware Cloud on AWS SDDC
- *Planning center* is always lowercase except when it appears as a UI label
- *Migration advisor* (lowercase) refers to the advisor tool generically; specific advisors are named by target (e.g., "Amazon EVS migration advisor")
- *Onboarding advisor* is the legacy term used in file names for the VMware Cloud on AWS and EC2 advisors; current UI labels use "migration advisor"
- Permission modes in Workload Factory: *Basic mode* (no credentials), *read-only mode*, *read/write mode*

**Technical constraints:**
- Up to four FSx for ONTAP volumes can be attached to a single vSphere cluster on VMware Cloud on AWS
- Well-architected scans run once per day automatically; on-demand scans are not supported
- The data collector script requires Microsoft PowerShell and VMware PowerCLI; SSL certificate checking must be disabled and unsigned scripts must be allowed
- Daily statistics collection with the data collector script requires vSphere statistics level 3 or above

### Typical user workflows

**Migrate to Amazon EVS:** Log in to Workload Factory → Upload VM inventory data → Launch EVS migration advisor → Specify configuration options and select VMs → Review deployment plan → Deploy FSx for ONTAP file system → Review well-architected insights

**Migrate to Amazon EC2:** Log in to Workload Factory → Upload VM inventory data → Launch EC2 migration advisor → Review deployment plan → Deploy FSx for ONTAP file system

**Migrate to VMware Cloud on AWS:** Log in to Workload Factory → Upload VM inventory data → Launch VMware Cloud migration advisor → Review deployment plan → Deploy FSx for ONTAP file system → Connect FSx for ONTAP to SDDC → Migrate VM data

**Migrate to Google Cloud VMware Engine:** Log in to Workload Factory → Upload VM inventory data → Launch GCVE migration advisor → Review deployment plan

**Review EVS well-architected status:** Discover EVS environment in Workload Factory → Wait for automatic daily scan → Open Well-architected status tab → Review findings by configuration area → Follow step-by-step remediation procedures
