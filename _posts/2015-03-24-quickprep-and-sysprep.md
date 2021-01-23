---
layout: post
title: "QuickPrep and Sysprep"
excerpt: "QuickPrep vs Sysprep. Good info to keep in your pocket"
tags: [quickprep, sysprep, VM]
comments: true
image:
  feature: vSphere6.0.jpg

---

[Jason Boche](http://www.boche.net/blog/) has a great post on [QuickPrep and Sysprep](http://www.boche.net/blog/index.php/2013/05/02/quickprep-and-sysprep/) and their differences.

He references [VMware KB 2003797](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003797) which states: 

> QuickPrep is a VMware system tool executed by View Composer during a linked-clone desktop deployment. QuickPrep personalizes each desktop created from the Master Image. Microsoft Sysprep is a tool to deploy the configured operating system installation from a base image. The desktop can then be customized based on an answer script. Sysprep can modify a larger number of configurable parameters than QuickPrep.

The below table outlines the key differences between QuickPrep and Sysprep:

| Function | QuickPrep | Sysprep |
|:--------|:-------:|--------:|
| Removing local accounts   | No | Yes |
| Changing Security Identifiers (SID) | No | Yes |
| Removing parent from domain | No | Yes |
| Changing computer name | Yes | Yes |
| Joining the new instance to the domain | Yes | Yes |
| Generating new SID | No | Yes |
| Language, regional settings, date, and time customization | No | Yes |
| Number of reboots | 0 | 1 (seal & mini-setup) |
| Requires configuration file and Sysprep | No | Yes |

