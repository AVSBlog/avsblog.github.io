---
layout: post
title:  "Ready, Set, Go ... Deploy AVS"
author: tredavis
categories: [ AVS, "Azure VMware Solution", Script, "vSphere", Microsoft, Azure, Lab]
image: assets/images/posts/2021-01-13/readysetgo.png

---

*By: Trevor Davis, Azure Global Blackbelt - Azure VMware Solution - [@vTrevorDavis](https://twitter.com/vtrevordavis)*

OK, so you want to deploy AVS.  Great!  Now what is the most efficient way to do it?  

As luck as it there is some pretty good documentation out there.  

First things first, you need to start with collecting up all the pre-requisites.  There isn't much, but it's very important.  Generally speaking most can be done on the fly assuming the person doing the deployment has at least Contributor rights to Azure and understands the overall Azure standards that their company has put in place.  [The complete list of pre-requisites can be found here](https://docs.microsoft.com/en-us/azure/azure-vmware/production-ready-deployment-steps).

The ones which absolutely need to be done ahead of time are [getting AVS quota added to your subscription](https://docs.microsoft.com/en-us/azure/azure-vmware/enable-azure-vmware-solution), [define the IP address segment to be used for AVS infrastructure](https://docs.microsoft.com/en-us/azure/azure-vmware/production-ready-deployment-steps#ip-address-segment) and [work out the ExpressRoute Gateway setup for Azure VMware Solution](https://docs.microsoft.com/en-us/azure/azure-vmware/production-ready-deployment-steps#azure-virtual-network-to-attach-azure-vmware-solution).

Once all those pre-requiretes have been identified, you can move on to the deployment.  

There are two ways you can do the deployment, you could do it [via the Azure Portal](https://docs.microsoft.com/en-us/azure/azure-vmware/deploy-azure-vmware-solution) or via a [Powershell deployment script](https://avs.ms/avspcdeployscript/).

After the deployment is done, you most likely will want to [connect Azure VMware Solution back to your on-premises environment via ExpressRoute](https://docs.microsoft.com/en-us/azure/azure-vmware/azure-vmware-solution-on-premises).  This step is not a requirement, you do have the option to stop at the previous step and just access the environment via the jumpbox in Azure.  If you did that, you have full functionality of Azure VMware Solution, w/ the exception of a network path back to your on-premises environment.

You may want to check out the [Azure VMware Solution Hands on Lab](https://my.vmware.com/web/vmware/evalcenter?p=azure-sol-hol-lightning-21), and also give a read to [Emad Younis'](https://twitter.com/emad_younis) blog post [Overview of Azure VMware Solution Next Evolution](https://emadyounis.com/overview-of-azure-vmware-solution-next-evolution/).  He does a great job going over the deployment in detail, as well as post deployment and benefits which are unique to Azure VMware Solution.
