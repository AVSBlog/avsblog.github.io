---
layout: post
title:  "Azure VMware Solution Deployment Script"
author: tredavis
categories: [ AVS, "Azure VMware Solution", Script, "vSphere", Microsoft, Azure, Lab]
image: assets/images/posts/2020-12-09/avspcdeploy2.png

---

*By: Trevor Davis, Azure Global Blackbelt - Azure VMware Solution - [@vTrevorDavis](https://twitter.com/vtrevordavis)*

This script will prompt for the inputs, validate your subscription is enabled for deployment and then deploy an Azure VMware Solution Private Cloud.  

After completion there will be a summary of the Private Cloud after deployment (see image below).

Going to work to add some post deployment add-ons soon.  But in the meantime, hope this may provide some value.

PLEASE NOTE: The following are requirements of the script.x

[Powershell 7](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-7.1#installing-the-msi-package)
[Azure Powershell](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps)
[Az.VMWare cmdlets](https://docs.microsoft.com/en-us/powershell/module/az.vmware/)

[https://github.com/tredavismicrosoft/scripts/blob/main/AVS_PC_Deploy.ps1](https://github.com/tredavismicrosoft/scripts/blob/main/AVS%20Private%20Cloud%20Deployment/AVS_PC_Deploy.ps1)

![Output](/assets/images/posts/2020-12-09/avspcdeploy2.png)
