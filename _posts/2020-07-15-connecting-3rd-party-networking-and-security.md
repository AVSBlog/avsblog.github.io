---
layout: post
title:  "Azure VMware Solution (AVS): Connecting 3rd Party Networking and Security Platforms"
author: tredavis
categories: [ AVS, "Azure VMware Solution", "nsx-t", "nsx", "VMWare" ]
image: assets/images/posts/2020-07-15/3rd-party-networking-1.png
---
*By: Gourav Bhardwaj (VMware), Trevor Davis (Microsoft) and Jeffrey Moore (VMware)*

## Challenge
When moving to Azure VMware Solution (AVS) customers may want to maintain their operational consistency with their current 3rd party networking and security platforms.  The types of 3rd party platforms could include solutions from Cisco, Juniper, or Palo Alto Networks and the means for connectivity is independent of the NSX-T Service Insertion/Network Introspection certification process for vSphere or AVS.  The following is a use case based on an actual customer deployment.

## Solution
The Azure VMware Solution environment allows access to the following VMware management components:

- vCenter User Interface (UI)
- NSX-T Manager User Interface (UI)

Within this architecture design, the uplink of the 3rd party appliance can be connected to a segment that is attached to the NSX-T “Tier 1” router while the individual or trunked downlinks of the appliance will support the connectivity of the Virtual Machine (VM) workloads which is similar to the On-Premises deployment model as depicted in the following diagram:

![Deployment Model for Connectivity of a 3rd Party Appliance with NSX-T](/assets/images/posts/2020-07-15/3rd-party-networking-1.png)

Once the appliance is attached to the NSX-T “Tier 1” router, static routes need to be configured to direct traffic through the 3rd Party appliance. Within the NSX-T Manager UI, the customer has the ability to create these static routes on the NSX-T “Tier 1” router which will assist in the network traffic direction through the 3rd Party appliance and to the customer’s VM workloads within AVS. Once the static routes are created, they can be redistributed within the dynamic routing protocol, Border Gateway Protocol (BGP).

This would allow for the static route information to be dynamically sent from the NSX-T “Tier 0” router through the uplink to the Top of Rack (ToR) platform and eventually, to the Azure Express Route backbone which will allow for the end-to-end connectivity from the customer’s locally attached On-Premises Express Route service to the AVS environment. This approach would provide a means to maintain the operational consistency between what is currently On-Premises and the Azure VMware Solution environment.

![Operational Consistency Deployment Model of 3rd Party Appliance in Azure VMware Solution](/assets/images/posts/2020-07-15/3rd-party-networking-2.png)

An additional consideration for this design is related to the location of the VM’s within the cluster and the potential vSphere Distributed Resource Scheduler (DRS) event which attempts to load balance the VM’s across the ESXi hosts within a cluster via vMotion based on available resources.  During such as event, the 3rd Party appliance may reside on one ESXi host while the VM workload resides on another ESXi host.  Within a customer’s On-Premises data center, this situation can be resolved by stretching the VLAN’s on the ToR switch that are associated to the uplinks and downlinks attached to the 3rd Party platform which would provide connectivity independent of which ESXi host the platforms and VM’s reside.  Within Azure VMware Solution, this needs to occur as well using NSX Segments or vSphere Distributed Switch (VDS). 

Once the solution is verified based on these mentioned topics, the customer is able to consume the 3rd Party platform within Azure VMware Solution in the same way as the On-Premises data center environment which will align with the requirement for operational consistency between On-Premises and AVS for services such as Disaster Recovery.

### Author Bio’s:

**Gourav Bhardwaj**

Staff Cloud Solutions Architect (VMware)  
VCDX 76 (VCDX-xx)  
Digital and workspace transformation expert; Speaker at conferences and workshops.  
LinkedIn: https://www.linkedin.com/in/vcdx076/  

**Trevor Davis**

Azure VMware Solution, Sr. Technical Specialist (Microsoft)  
Twitter: @vTrevorDavis  
LinkedIn: https://www.linkedin.com/in/trevorpdavis/  

**Jeffrey Moore**

Staff Cloud Solutions Architect (VMware)  
3xCCIE (#29735 - RS, SP, Wireless), CCDE (2013::20)  
Focused on incubation and acceleration efforts for Azure VMware Solution (AVS).  
LinkedIn: https://www.linkedin.com/in/jjtm/  
Twitter: @Jeffrey_29735  