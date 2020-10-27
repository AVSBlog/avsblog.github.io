---
layout: post
title:  "Azure VMware Solution and Azure FileSync"
author: tredavis
categories: [ "AVS", "Azure", "Azure VMware Solution", "Microsoft", "Azure Files", "tredavis", "VMWare", "Azure Filesync" ]
image: assets/images/posts/2020-03-24/1.png
---
*By: Trevor Davis (Microsoft)*

## Challenge

AVS (like all other hyperscale cloud providers) is architected on a hyper-converged platform, because of this any workload can be moved and performance many times increases due to the locality of disk I/O.  However, horsepower (vCPU/vMem) scale in parallel with storage.  Many times organizations find themselves in a situation where storage space needed drives the size of the cluster well beyond what they would need for horsepower. 

Upon deeper investigation into this challenge, many times file services are driving a considerable amount of the overall storage consumption.  File services are now a roadblock to move their VMware workloads to AVS.

Easy fix right?  Categorize what can be deleted (and delete it), ID what is needed to run the business on a day to day basis and then archive the rest.  Oh, and put in an operational model which now allows the organization to maintain moving forward.   

This is never going to happen in the majority of businesses and if it does, it's nothing which can happen in a short period of time.

## Solution

Azure VMware Solution and Azure Files.

By combining these two solutions organizations can realize a vSphere based cloud solution with a simple lift and shift, no re-platforming, no IP changes, no architecture changes. Additionally, storage footprint is shrunk in vSphere but no change what-so-ever to the file server hierarchy, security or files made available.


To deliver the solution Azure FileSync is installed on the File Servers before the migration to AVS, all files are sync'd to Azure File Storage. As files are needed, they are pulled down to the file server and kept locally for a pre-determined amount of time, as they become "cold" again, they are removed from the File Server freeing up space.​​​​​​

The following few sections will have a narrow focus on Azure Files and AVS, for a great blog series which goes into deep detail on Azure Files check out my colleague John Kelbley's blog series [Part 1](https://azureninjas.com/avoid-defer-costly-storage-upgrades-with-azure-file-sync-part-1/), [Part 2](https://azureninjas.com/avoid-defer-costly-storage-upgrades-with-azure-file-sync-part-2/), [Part 3](https://azureninjas.com/avoid-defer-costly-storage-upgrades-with-azure-file-sync-part-3-low-downtime/)

## How Does Azure FileSync Work and Help AVS?
 
Azure FileSync is installed on the File Servers, all files are sync'd to Azure File Storage.

As files are needed, they are pulled down to the file server and kept locally for a pre-determined amount of time, as they become "cold" again, they are removed from the File Server freeing up space.

Regardless of where the files sit, the File Server hierarchy is presented on the file server as it always has been.

<iframe width="1110" height="625" src="https://www.youtube.com/embed/2MMFTZt7tCU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In the configuration show below in Figure 1 we see a typical layout of an AVS environment; six hosts and a series of VMs running on vSphere/vSAN. What you will notice is that File Servers consumption of the vSAN datastore is approximately 40%.

This is driving the need for an additional two AVS nodes.

![1](/assets/images/posts/2020-03-24/1.png)

When leveraging Azure FileSync the cluster can be shrunk by two nodes, but no change to the architecture of the File Server landscape is required.

You will notice in Figure 2 below that instead of six hosts, there are four, however because Azure FileSync is being used the physical storage space on the vSphere cluster required to support file services is reduced dramatically, thereby allowing for the reduction of two nodes.

![2](/assets/images/posts/2020-03-24/2.png)

## AVS and Azure FileSync in Action

Now in this section lets look how the above is achieved.  On the left side of Figure 3 below you see a typical file hierarchy on a Windows File Server sitting inside of AVS Private Cloud. On the right the Azure Files Fileshare which is sitting in your Azure subscription.

You will notice that after the File Servers are Sync'd With Azure Files the same hierarchy is maintained between the File Server and Azure.

![3](/assets/images/posts/2020-03-24/3.png)

When we look at the entire used space on the file server on the left in Figure 4 below (the E: Drive) you will notice that the consumption of diskspace is 762 MB, but in Azure the consumption is 52 GB.

![4](/assets/images/posts/2020-03-24/4.png)

Here in Figure 5 below you will see that on the left is what the video file consumed before it was opened is 4kb.  After running the video for a minute or so the size on disk grew to 28 MB.

When that video file becomes "cold", you will see the size to fall back to the size it consumed on the left.​​​​​​​

![5](/assets/images/posts/2020-03-24/5.png)

## Conclusion

Through modernization of file services via Azure FileSync organizations enable a more efficient and cost effective migration to Azure VMware Solution.
