---
layout: post
title: "Autogrow vCenter Partitions"
excerpt: "Some vCenter partitions are painfully small. Let's grow them!"
tags: [vCenter, partitions, size, disk, lvm, autogrow]
comments: true
image:
  feature: vSphere6.0.jpg

---


When you deploy a vCenter Server Appliance it creates 10 hard disks for it's deployment. Often this automatic process is fine, but sometimes those partitions aren't large enough.

One partition in particular has been a pain point for me both in past as well as very recently. It's the `/storage/log` partition. Why only 10GB? I have a vCenter support log bundle that is well over 6.5GB in size when generated. Of course this fills up the partition and generates several vCenter alarms as well as doesn't allow the support bundle to be generated fully without corruption.

This has led to a support call with VMware to see what's needed to address this issue.

I'll outline what exactly I did to remediate this, please note though, your milage may vary.

1. Figure out what disk you wish to resize
  * For my specific issue, it was disk 5.
2. Resize that disk.
  * In this case, the disk was 10GB and I resized it to 20GB.
3. SSH to vCenter and get to bash shell
4. Run `df -h` to verify the size before any operations are run
5. Execute the autogrow command
  * `vpxd_servicecfg storage lvm autogrow`
  * Wait for `VC_CFG_RESULT=0`
6. Run `df -h` to verify the partition grew
7. High-five yourself. You did it.

William Lam: [Increasing disk capacity simplified with VCSA 6.0 using LVM autogrow](http://www.virtuallyghetto.com/2015/02/increasing-disk-capacity-simplified-with-vcsa-6-0-using-lvm-autogrow.html)
