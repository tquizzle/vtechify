---
layout: post
title: "How to upgrade from vCSA 5.x and/or 6.x to vCSA 6.0 U1"
excerpt: "Quite a few folks are in this arena. You need to update to vCSA 6.0 U1 and here's how to do just that."
tags: [vSphere, upgrade, vCSA, vCenter, ESXi]
comments: true
image:
  feature: vSphere6.0.jpg

---

Thanks to William Lam, this is well documented.

> - If you have an External PSC with your VCSA 6.x and wish to upgrade, the process shown below is the same for both the PSC and the VCSA. You will want to first upgrade your PSC first as that provides authentication to your vCenter Server. Once the PSC has been upgraded and accessible on the network again, you will then want to move to your VCSA. If you are interested in the proper sequence and ordering of VMware Products to update, you can also check out this handy [VMware KB 2109760](http://kb.vmware.com/kb/2109760) which provides all the details
> - Thanks to fellow reader Idan for reporting this but it looks like after an upgrade of the VCSA, the default VMware URL for the VAMI is not working. You will need to update it to point to the following URL **https://vapp-updates.vmware.com/vai-catalog/valm/vmw/647ee3fc-e6c6-4b06-9dc2-f295d12d135c/6.0.0.10000.latest/** instead of the default one as shown in the screenshot below. This is only applicable for upgrade scenarios. If you deploy a new VCSA 6.0 Update 1, it will automatically be using the correct URL
> ![Update Settings](http://www.virtuallyghetto.com/wp-content/uploads/2015/09/incorrect-vami-repo-url.png)
> - Ensure you have a proper backup and take a snapshot of your VCSA 6.x appliance before beginning.
> - Download the VCSA 6.0 Update 1 _Full Patch_ (VMware-vCenter-Server-Appliance-6.0.0.10000-3018521-patch-FP.iso) by visiting the [VMware Patch Download site](https://my.vmware.com/group/vmware/patch).
> ![vCSA6.0 to vCSA 6.0 U1](http://www.virtuallyghetto.com/wp-content/uploads/2015/09/upgrade-from-vcsa-6.0-to-vcsa-6.0-update-1-0.png)
> - Mount the VCSA 6.0 Update 1 Patch ISO to your VCSA 6.x appliance using either the vSphere Web/C# Client
> - Login to your VCSA 6.x appliance via SSH to the appliancesh interface. If you have disabled that, simply type "appliancesh" and login with the root credentials.
> - Run the following command to stage and install the patches from the VCSA 6.0 Update 1 Patch ISO:
> {% highlight powershell %}
software-packages install --iso --acceptEulas
{% endhighlight %}
> ![](http://www.virtuallyghetto.com/wp-content/uploads/2015/09/upgrade-from-vcsa-6.0-to-vcsa-6.0-update-1-1.png)

> If you run into any errors while either staging or installing the patches, you should drop into the bash shell and take a look at **/var/log/vmware/applmgmt/software-packages.log** file for additional information. One common issue that I have seen in the past is if your /storage/log partition is full and you may need to perform a clean up before continuing.
{: .notice}

> - Once the upgrade has completed, you just need to reboot your VCSA by running the following command:
{% highlight powershell %}
shutdown reboot -r "Updated to vSphere 6.0u1"
{% endhighlight %}

> - A quick way to confirm that you have successfully upgraded your VCSA to vSphere 6.0 Update 1, simply open a browser to the following URL: https://[VCSA-IP]:5480 and it should take you to the new HTML5 VAMI interface.


Check out William's post using this sweet-ass button! <a href="http://www.virtuallyghetto.com/2015/09/how-to-upgrade-from-vcsa-5-x-6-x-to-vcsa-6-0-update-1.html" class="btn btn-success">virtuallyGhetto</a>
