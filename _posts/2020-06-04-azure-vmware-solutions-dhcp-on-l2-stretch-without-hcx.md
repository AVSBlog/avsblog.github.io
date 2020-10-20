---
layout: post
title:  "Azure VMware Solutions: DHCP on L2 Stretch w/ HCX"
author: tredavis
categories: [ "AVS", "Azure", "Azure VMware Solution", "Microsoft", "DHCP", "tredavis", "VMWare", "HCX", "L2 Stretch" ]
image: assets/images/posts/2020-06-04/step1.jpg
---
*By: Trevor Davis (Microsoft)*

## Challenge

By default ​​​​​​​DHCP will not work for VMs on the HCX L2 stretch network in Azure VMware Solutions when the DHCP server lives in the organization's on-premises datacenter.  This is because NSX by default will block all DHCP requests from traversing the L2 stretch.  But not to worry, there is a very simple solution.
 
## Step 1: Get Destination Network Name

Go to you source vCenter (typically on-prem) and find the network extension which needs to support DHCP requests from AVS to On-Prem.  Take note of the destination network name.

![step1](/assets/images/posts/2020-06-04/step1.jpg)

## Step 2: Create a Segment Security Profile

Log into the NSX Manager in AVS.  Navigate to Networking, Segments, Segment Profiles and then Add Segment Profile.  You will need to choose the Segment Security profile.

![step2](/assets/images/posts/2020-06-04/step2.jpg)

## Step 3: Configure the Segment Security Profile (Part 1)

Assign a name and a tag to the profile, then make all the toggles look exactly as shown in this picture.

![step3](/assets/images/posts/2020-06-04/step3.jpg)

## Step 4: Configure the Segment Security Profile (Part 2)

In this step you are going to need to remove all the MAC addresses (if any) which are listed in the BPDU Filter Allow List.  After removing, your screen should look exactly as it does in this picture.

![step4](/assets/images/posts/2020-06-04/step4.jpg)

## Step 5: Edit the Network Segment  

Go back to the Networking Tab, choose Segments on the left column, Segments, then in the search area on the right enter the name of the network (from step 1).  The search should then find the network, when it goes edit the segment by choosing the 3 button icon and choose Edit.
 
![step5](/assets/images/posts/2020-06-04/step5.jpg)

## Step 6: Change the Segment Security

Change the Segment Security option from whatever it is currently to the item you created in step 3b.  Save the configuration. 

![step6](/assets/images/posts/2020-06-04/step6.jpg)

## Conclusion

That's it, by modifying the AVS NSX configuration, DHCP requests will now be sent from the VM in AVS on the L2 stretch back to on-prem DHCP server.  