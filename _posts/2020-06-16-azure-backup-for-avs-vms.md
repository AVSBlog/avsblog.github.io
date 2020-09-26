---
layout: post
title:  "Azure Backup for Azure VMware Solutions Virtual Machines"
author: tredavis
categories: [ AVS, "Azure VMware Solution", "Azure Backup", "tredavis", "VMWare" ]
image: assets/images/posts/2020-06-16/2020-06-16.png
---

Azure Backup for Azure VMware Solutions Virtual Machines
## Challenge 
You have vSphere-based workloads running in Azure on Azure VMware Solutions (AVS).  But of course, things happen, and backups of these virtual machines (VMs) are still a requirement. 

 

One choice would be to use the existing on-premises backup solution and backup the VMs from AVS to on-premises.  For multiple reasons that would not be the ideal solution, most importantly proximity to workloads and cost. 

 

In general, there will be charges incurred when taking data from Azure and pulling it back to on-premises.  Pulling all backup data daily from Azure to on-premises would not be an ideal situation financially or architecturally.

 

## Solution
One of the major benefits of VMs running on vSphere in Azure is the proximity and integration with Azure services. 

 

Knowing that backups are a critical need for AVS workloads, Microsoft have integrated Azure VMware Solutions with Azure Backup. 

 

Let's look at the high-level architecture, installation, and some key features.

 

## Architecture
![Architeture](/assets/images/posts/2020-06-16/2020-06-16.png)

While not detailed, this picture hopefully provides a good overview.  The Microsoft Azure Backup Server (MABS) integrates with vCenter server in AVS.  VM backups are written to the MABS, and the MABS integrates with Azure Recovery Services Vault to store recovery points of the backups (more detail on this later).

 

Using Azure Recovery Services Vault allows for backups to be stored on low cost Azure storage for long term retention and recovery. 

 

## Installation
After AVS is deployed, the following steps will enable Azure Backup for the vSphere VMs running in AVS.

1. [Build a Windows VM which will be used to deploy the Microsoft Azure Backup Server (MABS).](https://docs.microsoft.com/en-us/azure/azure-vmware/set-up-mabs-for-avs#determine-the-size-of-the-virtual-machine)
2. [Create a Azure Recovery Services Vault.](https://docs.microsoft.com/en-us/azure/azure-vmware/set-up-mabs-for-avs#create-a-recovery-services-vault)
3. [Install Microsoft Azure Backup Server.](https://docs.microsoft.com/en-us/azure/azure-vmware/set-up-mabs-for-avs#download-and-install-software-package)
4. [Connect MABS to vCenter in AVS.](https://docs.microsoft.com/en-us/azure/azure-vmware/backup-avs-vms-with-mabs#create-a-secure-connection-to-the-vcenter-server) 
5. [Configure and protect your vSphere VMs to Azure Backup.](https://docs.microsoft.com/en-us/azure/azure-vmware/backup-avs-vms-with-mabs#configure-a-protection-group)

For a detailed guide on how to install and operationalize Azure Backup and AVS please check out https://docs.microsoft.com/en-us/azure/azure-vmware/set-up-mabs-for-avs

 

## Key Features
 

**Agentless Backup**: To backup vSphere-based VMs, Azure Backup __does not__ require an agent installed on vCenter, vSphere Hosts or vSphere VMs.

 

**Cloud-Integrated Backup**: For short term storage Azure Backup Server backs up data to disk. Additionally, for both short and long term backup Azure Backup Server protects workloads to low cost Azure storage.  Notice is the graphic below that Microsoft Azure Backup Server is connected to Azure Recovery Services Vault by evidence that the VM with the name _"FileServerOnAVS"_ is represented as part of the Protection Group on the backup server, but also showing in the Recovery Services Vault, which is backed by low cost Azure Storage.

![AzureStorageIntegration](/assets/images/posts/2020-06-16/azurestorageintegration.png)

 

 

**Detect and Protect VMs**: New VMs created on the vSphere Cluster in AVS can be detected automatically and have a protection policy applied.  

![autodetect](/assets/images/posts/2020-06-16/autodetect.png)

 

 

**File or Full VM Recovery**: Azure Backup Server can recover files/folders from a Windows VM without recovering the entire VM, or if needed the entire VM can be recovered.  You will see in the graphic below that the backup of _"FileServerOnAVS"_ allows for granular file recovery or recovery of the entire VM.

![File or Full VM Recovery](/assets/images/posts/2020-06-16/both.png)

 

 

**Create Protection Groups Easily**: Because of the tight integration with vCenter and AVS, when creating Protection Groups, VMs can be selected granularly or by larger groupings like Folders.

![Protection Group](/assets/images/posts/2020-06-16/protectiongroup.png)

## Learn More
By no means was that an exhaustive review of Azure Backup and Azure VMware Solutions integration, but hopefully you can see the value it can bring to your Azure based vSphere Cluster.  Please review [this link](https://docs.microsoft.com/en-us/azure/azure-vmware/set-up-mabs-for-avs) for more information.