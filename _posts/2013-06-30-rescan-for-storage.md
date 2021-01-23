---
layout: post
title: "Rescan for Storage"
excerpt: "I always forget the syntax for how to rescan a host for new storage."
tags: [PowerCLI, rescan, storage, HBA]
comments: true
image:
  feature: vSphere6.0.jpg
---


I always forget the syntax in PowerCLI for rescaning a host for new storage.

{% highlight powershell %}
Get-VMHost | Get-VMHostStorage -RescanAllHBA -RescanVMFS
{% endhighlight %}
