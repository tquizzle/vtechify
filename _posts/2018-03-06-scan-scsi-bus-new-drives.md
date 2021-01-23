---
layout: post
title: Scan SCSI bus for new drive
excerpt: "When adding a new disk to a Linux VM, you usually have to reboot for the system to recognize the disk. Now you don't have to."
tags: [scan, reboot, linux, scsi]
modified: 2014-09-14
comments: true
---

Recently when adding a new disk to a VM, a colleague of mine suggested a new trick.

"You don't have to reboot", he said, "just do this!"

~~~bash
for BUS in /sys/class/scsi_host/host*/scan
> do
>    echo "- - -" >  ${BUS}
> done
~~~


Now you can go about fdisk and formatting your disk.
