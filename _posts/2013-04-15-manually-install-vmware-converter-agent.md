---
layout: post
title: "Manually Install VMware Converter Agent"
excerpt: "Pre-Install the VMware Converter Agent to avoid problems during P to V conversions."
tags: [Agent, converter, vCenter]
comments: true
image:
  feature: vSphere6.0.jpg
---

<figure>
	<img src="http://i1.wp.com/lantechca.files.wordpress.com/2013/03/image20.png">
</figure>

Today I really needed to jump on a P to V conversion. This hardware was dropped in my lap and I didnt have much time to get it configured. As luck would have it, I also couldn’t connect to the ADMIN$ share. Which means that the vCenter Standalone Converter couldn’t copy the files necessary to install the agent and begin the conversion. Thanks to [cat brain](http://www.userdel.com/post/3345504444/manually-install-vmware-converter-agent-for-windows), I was able to quickly get this going.

> On the server you have VMWare Converter standalone installed, go to “C:\Program Files (x86)\VMware\VMware vCenter Converter Standalone” – obviously substitute the correct driver letter and if you’re not on a 64bit box you can remove the “(x86)” part.
Find the file named “VMware-Converter-Agent.exe” and copy it over to the Windows box.
Run the executable you copied.
