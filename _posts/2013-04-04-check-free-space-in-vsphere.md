---
layout: post
title: "Check Free Space in vSphere"
excerpt: "Checking for Free Space is easy"
tags: [free space, storage, vSphere, ESXi]
comments: true
image:
  feature: vSphere6.0.jpg
---

I had an issue recently where I needed to check the file space on an ESXi host. Luckily [krypted.com](http://krypted.com/vmware/checking-free-space-in-esx/) landed in my Google search with just what I needed.

 
> Most of us will be familiar with the df command. But in ESX, you use the vdf command, located in /usr/sbin. Running the vdf command will net you similar output to what you see with df. Simply run the following to see free space on each of your disks:

{% highlight bash %}
vdf -h
{% endhighlight %}

You can also list all of your data stores to correlate the vdf output with esxcfg:

{% highlight bash %}
/usr/sbin/esxcfg-scsidevs -c
{% endhighlight %}

