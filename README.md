# IT-Portfolio
A hands-on portfolio of IT projects — cloud deployments, networking, and systems administration documented with step-by-step write-ups and screenshots.

## Projects

| # | Project | Tools/Tech | Summary |
|---|---------|-----------|---------|
| 01 | [Deploying a Virtual Machine in Azure](Projects/01-Azure-VM-Setup/README.md) | Azure, RDP, NSG, Windows Remote Desktop App | Provisioned and secured a Windows VM in Azure, restricted RDP access via NSG rules, and connected remotely. |
| 02 | [Active Directory Domain Setup in Microsoft Azure](Projects/02-Active-Directory-Domain-Setup/README.md) | Azure, Windows Server, AD DS, DNS, Group Policy, Password Reset | Deployed a Domain Controller, joined a client VM, created users/OUs, and applied Group Policy across the domain. |
| 03 | [Bulk Active Directory User Creation via PowerShell](Projects/03-bulk-ad-user-creation-powershell/README.md) | PowerShell, Active Directory, CSV | Automated bulk AD user creation from a CSV, including OU routing and random password generation. |
| 04 | [Standalone DNS Server & Zone Configuration](Projects/04-dns-server-configuration/README.md) | Windows Server, DNS | Deployed a standalone DNS server, configured a custom zone with A, CNAME, MX, and TXT records, and set up forwarding. |
| 05 | *Coming soon* | Azure, VNet, VLANs | Network segmentation lab using VLANs and firewall rules. |
| 06 | [Azure Monitor & Alerting for VM Resource Thresholds](Projects/06-azure-monitor-alerting/README.md) | Azure Monitor, Alerts, Action Groups, PowerShell | Configured a full monitoring and alerting pipeline for an Azure VM, verified end-to-end with a real CPU spike and email notification. |
| 07 | *Coming soon* | Splunk | SIEM setup for centralized log correlation and threat detection. |
