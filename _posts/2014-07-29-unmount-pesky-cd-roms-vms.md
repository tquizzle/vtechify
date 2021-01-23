---
layout: post
title: Unmount pesky CD-ROMs from VMs
excerpt: "Get rid of those CD-ROMs that seem to stick around."
modified: 2014-07-30
tags: [CDROM, PowerCLI, Unmount]
comments: true
image:
  feature: vSphere6.0.jpg
---

Sometimes you need to quickly remove CDROMs from VMs to not violate vMotion or just because you're lazy and forgot to unmount them when you were finished. Either way, those CDROMs should not be forever mounted to your VMs. This can only cause problems for you in the future.

So, if you need a quick PowerCLI one-liner to do that for you, look no further.

{% highlight powershell %}
Get-VM <vmNames> | Get-CDDrive | Set-CDDrive -NoMedia -Confirm:$false
{% endhighlight %}
