---
layout: post
title:  "Connect to Azure VMware Solution (AVS) using VPN"
author: carlosv
categories: [ AVS, "Azure VMware Solution", "vWAN", "VPN", "VNET" ]
image: assets/images/posts/2020-09-15/vwan-1.png
---

*By: Trevor Davis @tredavis and Carlos Villuendas @CarlosV*

## Challenge

ExpressRoute is the preferred method to connect the customer's on-premises environment to Azure VMware Solution (AVS), but what happens if you do not have access to ExpressRoute?

## Solution

Connect your on-premises site to AVS using VPN and Azure Virtual WAN.

Azure Virtual WAN allows transit connectivity between VPN and ExpressRoute. This implies that VPN-connected sites can communicate with ExpressRoute-connected sites.

Reference: https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-about#transit-er

NOTE: Azure VMware Solution (AVS) is connected to the Azure backbone via an ExpressRoute.

## Architecture

![AVS - VPN vWAN](/assets/images/posts/2020-09-15/vwan-1.png)
 
## Important points

- VMware HCX is **not supported** by VMware over VPN. If the customer intends to migrate workloads from on-premises to Azure VMware Solution (AVS), another migration tool needs to be used.
- This configuration requires the **standard** Azure Virtual WAN type. Check [this article](https://docs.microsoft.com/en-us/azure/virtual-wan/upgrade-virtual-wan) for more details. 
- When connecting Azure Virtual WAN to a virtual network, make sure that the virtual network **does not have any virtual network gateways**. This is very important when planning the connection to an existing Azure environment. More details [here](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-site-to-site-portal#before-you-begin).

## Installation

After Azure VMware Solution is deployed, you can connect your on-premises environment to Azure VMware Solution (AVS) using VPN and Azure Virtual WAN following these steps.

1. Create an Azure Virtual WAN.
2. Create a hub.
3. Create a site.
4. Connect a VPN site to a hub.
5. Connect a Vnet to a hub (if needed)
6. Connect the ExpressRoute circuit to a hub.
 

Steps 1 to 5 are covered in this article: [Create a Site-to-Site connection using Azure Virtual WAN](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-site-to-site-portal)

Step 6 is covered in this article: [Create an ExpressRoute association using Azure Virtual WAN](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-expressroute-portal)

## Installation notes:

Format the VPN configuration file to make it more readable.

To configure your on-premises VPN device, you will need to download the VPN configuration from the Azure portal, instructions [here](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-site-to-site-portal#device). The configuration file will look like the following image. Use VS Code to format the configuration file to look like the example in [this article](https://docs.microsoft.com/en-us/azure/virtual-wan/virtual-wan-site-to-site-portal#example-device-configuration-file).

![VPN Config File](/assets/images/posts/2020-09-15/vwan-2.jpg)

You can connect multiple virtual networks to the virtual WAN hub, even virtual networks from different Azure subscriptions.  