# Project 01: Deploying a Virtual Machine in Microsoft Azure

## Objective
Deploy a Windows Server virtual machine in Microsoft Azure, configure secure remote access, and document the process end-to-end. Goal: build hands-on familiarity with Azure's VM provisioning workflow and basic network security controls.

## Tools & Technologies
- Microsoft Azure (Free Tier)
- Azure Virtual Machines
- Network Security Groups (NSG)
- Remote Desktop Protocol (RDP)

## Steps Taken

### 1. Created a Resource Group
Set up a dedicated resource group (`rg-portfolio-vm`) to keep all resources for this project organized and easy to tear down afterward.

![Resource group creation](images/01-resource-group.png)

### 2. Provisioned the Virtual Machine
Selected a Windows Server 2022 image, chose the B1s (free-tier eligible) size, and configured the admin username/password.

![VM creation blade](images/02-vm-create.png)

### 3. Configured the Network Security Group
By default, Azure opens RDP (port 3389) to the whole internet, which is a security risk. I edited the inbound rule to restrict RDP access to my home IP address only.

![NSG inbound rule restricted to my IP](images/03-nsg-rule.png)

### 4. Connected via Remote Desktop
Downloaded the RDP file from the Azure portal and connected using the credentials set during provisioning.

![Successful RDP connection to the VM](images/04-rdp-connected.png)

## Challenges & Troubleshooting
- Initially couldn't connect via RDP — traced it back to the NSG rule I'd set being scoped to the wrong IP (my home IP had changed since I last checked it). Fixed by re-verifying my current public IP and updating the rule.
- [Add any other real issues you hit]

## Outcome
Successfully deployed and secured a cloud VM, and gained a working understanding of how Azure handles resource grouping, VM provisioning, and network-level access control via NSGs.

## What I'd Do Next
- Automate this deployment using Azure CLI or an ARM/Bicep template instead of the portal UI
- Set up Azure Monitor/alerts on the VM
