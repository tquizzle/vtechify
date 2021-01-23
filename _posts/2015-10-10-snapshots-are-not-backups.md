---
layout: post
title: "Snapshots are NOT Backups"
excerpt: "Snapshots are NOT backups. If you think they are, you're doing it wrong."
tags: [vDP, vSphere, Backup]
comments: true
image:
  feature: vSphere6.0.jpg

---


I really like this post over at [digitalkungfu](https://digitalkungfu.wordpress.com/2015/10/03/snapshots-are-not-backups-or-vdp-and-you/). He outlines why snapshots should never be considered a backup.

Because of the ease of vDP from VMware with almost all licensing tiers, if you don't have a great solution for image and application level backups, this is a perfect product for you.

I've recently deployed one of these appliances at each of my production remote sites. Works like a charm.

> Working in production environments the constant challenge of maintaining uptime aka ‘steady-state’ but at the same slowly or as quick as feasible move forward with changing demands of the business.
> 
> Change can came in many forms. It is a driver for your organization.
> 
> A simple response to a vulnerability; patching is a necessity.
> 
> New features are required. Upgrades will be needed.
> 
> And more importantly disaster avoidance. The idea is to prepare in advance avoid disaster. It is akin to shift and dodge BEFORE some bump comes in the road. There are many approaches to this like having a stretched geo-location metro cluster.
> 
> Whatever the driver you have to have a fallback plan. If the post-change activity fails, if there is an unforeseen after-effect.. Things do not always work 100% as planned. What is your fallback plan? What? You have a VMware environment. You did click the snapshot button.. Well, that does work but it isn’t a full backup
> 
> From KB [1025279](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1025279)
> 
> - Snapshots are not backups. A snapshot file is only a change log of the original virtual disk.
> - Snapshots are not complete copies of the original vmdk disk files….it only copies the delta disks. The change log in the snapshot file combines with the original disk files to make up the current state of the virtual machine. If the base disks are deleted, the snapshot files are useless.
> - Delta files can grow to the same size as the original base disk file, which is why the provisioned storage size of a virtual machine increases by an amount up to the original size of the virtual machine multiplied by the number of snapshots on the virtual machine.
> - The maximum supported amount of snapshots in a chain is 32. However, VMware recommends that you use only 2-3 snapshots in a chain. — [ed The reason is there is a performance hit]
> In fact VMware recommendation is to setup an alarm in vcenter if the VM is running from a snapshot to avoid this condition
> 
> See KB [1018029](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1018029) - “Configuring VMware vCenter Server to send alarms when virtual machines are running from snapshots”
> 
> Now the question still remains.. What options do you have?
> 
> Well there is good news!! VMware as of March 1, 2015. “VMware vSphere Data Protection Advanced will be consolidated into VMware vSphere Data Protection (available through vSphere Essentials Plus Kit or higher vSphere editions, all vSphere with Operations Management editions and all vCloud Suite editions) and will no longer require purchase of a separate license. All functionality available with vSphere Data Protection Advanced, previously available as a standalone product, is now included in VMware vSphere Data Protection 6.0 – See more at: Announcement
> 
> WOOHOO.
> 
> Why is this cool? There are many reasons but to sum things up.
> 
> VMware Data Protection Advanced (VDP) is very cool. It is based on modern backup solutions.
> 
> - There are no tapes
> - There is deduplication – Variable length up
> - There is replication
> - File recovery
> - VM recovery
> - Application aware backups
> - Efficient, bandwidth throttling
> - Changed Block Tracking (CBT) Restore<br />
>   vSphere Data Protection uses Changed Block Tracking (CBT) during image-level backups. CBT is also utilized with image-level restores in some cases to improve speed and efficiency
> - It can plug into something really big (Data Domain and Avamar)
>  	- Data Domain allows for “Consolidate backup, archive, and disaster recovery with high-speed deduplication”
>  	- Avamar  DEDUPLICATION BACKUP SOFTWARE AND SYSTEM — VDP is based on Avamar. See the announcement.
> 
> It is super easy to install and use. I did say easy and it is, because you can even configure VDP to allow for.
> 
> - Linux-based virtual appliance: Easily install and configure backups.
> - Self-Service File Level Recovery: Enable guest OS administrators to restore individual files and folders.
> - Wizard-driven backup policies: Assign backup jobs to individual virtual machines or larger containers such as a cluster or resource pool, with specific schedules and retention policies.
> - There is no need for agents in the VM for normal backups.
> - Application aware backups. Backup agents for Microsoft SQL Server, Exchange, and SharePoint. The agents enable application consistent backup and recovery of these applications on virtual and physical machines
> 
> See more at: http://www.vmware.com/products/vsphere/features/data-protection.html

You can also see vDP from VMware's <a href="http://docs.hol.vmware.com/HOL-2012/HOL-PRT-02_EN/HOL-PRT-02-m4/lessons/VMware_VDP_Demo.html" class="btn btn-info">Hands On Labs</a>