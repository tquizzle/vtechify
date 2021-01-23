---
layout: post
title: "Rescanning VASA Providers"
excerpt: "Occasionally, vCenter will show you that all vSAN storage profiles are Not Applicable. Here's how to fix that."
tags: [vCenter, vSAN, VASA, Storage]
comments: true
image:
  feature: vSphere6.0.jpg

---
Have you ever been viewing the contents of your vCenter, and noticed that all of your VM's have a storage policy compliance of "Not applicable"?

This has happened to me several times and it's maddening. Especially when you know that they are configured properly.

Normal Google searches lead you to believe that it's because you configured a storage policy but the storage backend can't comply with the capabilities of the storage policy.

<blockquote>
A ‘Not Applicable’ state occurs when a VM Storage Policy with certain capabilities is applied to a virtual machine, but that virtual machine resides on storage which does not understand the capabilities. For instance, if I created a VM Storage Policy using VSAN capabilities like Number of Failures To Tolerate, or Number of Disk Stripes per Object, and then applied that policy to a virtual machine which is residing on a VMFS or NFS datastore, the Compliance Status would become ‘Not Applicable’.
</blockquote>
[Cormac Hogan's Amazing Blog](http://cormachogan.com/2014/04/03/vsan-part-22-policy-compliance-status/)


However in my case, I was indeed on the vSAN datastore and those policies were compliant yesterday. What happened? Re-applying the policy does not fix it. Nor does switching to a different policy. What to do?

## Rescan your Providers

What does it really do?
![Storage Providers]({{ site.url }}/images/vasa-storage-providers-1.png)

Login to vCenter and navigate to Hosts and Clusters. Select your vCenter from the top left and go to "Manage" then "Storage Providers."
Find the "Active" provider and rescan it. You're looking for the icon that I've zoomed in on below.

![Storage Providers]({{ site.url }}/images/vasa-storage-providers-2.png)

Give it a few minutes and all will be right with your policies.
