---
layout: post
title: Getting the Host Version of your ESXi Hosts
excerpt: "Quickly check what version of ESXi your hosts are running."
tags: [PowerCLI, Version]
modified: 2015-17-02
comments: true
image:
  feature: vSphere6.0.jpg
---

Ever needed to quickly find out what version your ESXi host were at? I sure did tonight while doing some upgrades and I didn't have time to check each host individually.

That's when this little gem helped out a ton:

{% highlight powershell %}
Get-View -ViewType HostSystem -Property Name,Config.Product | Select Name,($_.Config.Product.FullName) | Sort-Object Name
{% endhighlight %}
