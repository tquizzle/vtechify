---
layout: post
title: The Unfortunate Corrupted TCP Stack
excerpt: "No connection, not pingable, ICMP traffic drops...bad TCP stack on a VM."
tags: [tcp, corrupted, winsock, ipsec]
comments: true
image:
  feature: Windows.jpg

---

Today while troubleshooting an unpingable VM, there was just something not right about it.

<figure>
	<img src="http://cdn.arstechnica.net/09-29-2010/tcp_ip_stack.png">
	<figcaption><a href="http://cdn.arstechnica.net/09-29-2010/tcp_ip_stack.png" title="">TCP/IP Stack and OSI reference model - arstechnica</a>.</figcaption>
</figure>


We checked everything we could think of, then double-checked.

- distributed port group is good
- upstream switches are good
- other VMs on same host and network are good
- VM was good before last reboot...hmm

So that last one...seems that something went wrong once the VM tried to reboot after Microsoft patches.

After trying several things (I wont go into what all we tried) we stumbled across [this](http://technicalpath.blogspot.com/2008/06/case-of-corrupted-tcp-stack.html).

> First hint was the bad registry reading from HKLM\Software\Microsoft\IPSec....
>
> That possibly tells me that the IPSec in Windows 2003 server seem to be an issue that I'm dealing with...to ensure that this is the case, I launched the Registry Editing tool and notice that the keys under HKLM\Software\Microsoft\IPSec was not readable. By default, if IPSec is not turn on from the Windows FW, you should be able to view the hive of it with no value.

IPSec? Yes, it got jacked - polstore.dll somehow was corrupted.

1. Delete HKLM\Software\Microsoft\IPSec
2. From command prompt
  - Unregister the faulty driver: **regsvr32 /u polstore.dll**
  - Register the dll back to the system: **regsvr32 polstore.dll**
3. Reboot

Problem solved.