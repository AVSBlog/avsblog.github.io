---
layout: post
title:  "How to Migrate Legacy VMware Workload to Azure VMware Solution"
author: ravik
categories: [ AVS, "Azure VMware Solution", "legacy VMware", "Migration", "V2V Migration", "Hybrid Cloud Interconnect", "HCX", "VMware 4.x to VMware 5.x", "VMware 4.x to VMware 6.x" ]
image: assets/images/posts/2020-10-15/esxi-upgrade-for-hcx-front-cover.png
---

*By: Ravi Kaur @induswater_ravi*

## Challenge

Some customers have workloads that are currently hosted on legacy VMware environments which are not compatible with VMware Hybrid Cloud Interconnect (HCX). In order to save time and complexity, these customers are keen to use VMware HCX as the migration / mobility tool to migrate the virtual machines On-Prem to AVS and maintain the IP / MAC address. 

## Solution

Customers can use the interim V2V migrate methodology that will allow HCX compatibility for On Prem infrastructure. 

![ESXi Upgrade for HCX](/assets/images/posts/2020-10-15/esxi-upgrade-for-hcx.png)

## Unsupported VMware Infrastructure to Azure VMware Solution - Upgrade and Migration steps

Below are the complete list of steps that depict the migration path from On Prem legacy unsupported infrastructure to Azure VMware Solution

1.	Deploy ESXi 5.x / 6.x hosts and vCenter servers with evaluation license and configure vDS on same
2.	Create Swing Space that is presented to all ESXi hosts in both vSphere 4.x and vSphere 5.x / 6.x environment
3.	Virtual Machines that need to be migrated can be cloned and the clone can be placed in the swing space
4.	Cloned VM’s are accessed from the vCenter of 5.x / 6.x environment through the swing space
5.	After verifying the  cloned virtual machines in the 5.x / 6.x  environment, shut down the VM on the 4.x environment
6.	Start the clone of the virtual machine in the 5.x / 6.x environment and upgrade the VM Tools and Virtual Machine Hardware
7.	Conduct basic checks on the server and the application on the vSphere 5.x / 6.x infrastructure 
8.	Applications are now sitting on HCX supported VMware infrastructure and they can now be migrated into Azure VMware Solution
9.	Deploy AVS private Cloud in Azure and HCX Manager will be deployed in AVS
10.	Deploy HCX on Prem on the 5.x / 6.x vCenter server
11.	Log on to the 5.x / 6.x vCenter server On Prem and from the HCX plugin create a Site Pair between the On Prem and AVS in Azure
12.	Create Compute profile and network profile for the target environment that will be utilized by the virtual machines once on AVS
13.	Create a Service Mesh that will deploy HCX appliances on both the source and destination sites and automatically configure HCX to create the secure optimized transport fabric.
14.	Configure Layer 2 Network Extension for the VLANs that need to be used to maintain IP / MAC addresses of the On Prem VMs  
15.	LIVE vMotion or perform Bulk vMotion of VMs
16.	Access the migrated virtual machines in AVS and conduct basic checks on the server and application level
17.	Protect migrated Virtual machines using HCX / SRM / ASR

## V2V Migration - Pros

The V2V migration is a very simplified migration methodology that will allow customers to move to Azure VMware Solution at a fast pace

## V2V Migration - Cons

Minor downtime will be experienced by the applications. After cloning, application server will be shutdown in vSphere 4.x environment and the cloned VM will be started in the vSphere 5.x / 6.x environment

I hope this article has provided an insight towards simplfied interim upgrade On-Prem such that the VMware Infrastrucutre can be prepared for migration into AVS.