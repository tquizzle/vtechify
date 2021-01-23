---
layout: post
title: "vSphere Web Client cannot connect to vCenter Single Sign On server error"
excerpt: "Occasionally you might encounter an issue with the vSphere Web Client incapable of connecting to the vSphere SSO."
tags: [vSphere, Client, vCenter, Error]
comments: true
image:
  feature: vSphere6.0.jpg

---

![VMware vSphere Web Client Error](http://blog.mrpol.nl/wp-content/uploads/2015/03/031215_1530_Solvingthev1.png)
{: .image-pull-right}

I've seen this several time where a given vSphere Web Client cannot connect to the vCenter server or SSO server.

It's a simple fix, but one that frustrates you unless you already know the solution.

1. Go to the vCenter's VAMI interface - https://vcenter.fqdn:5480
2. Note that the vSphere Web Client service is probably running fine.
![Services](http://blog.mrpol.nl/wp-content/uploads/2015/03/031215_1530_Solvingthev2.png)
3. Stop / Start the vSphere Web Client Service
4. Grab a coffee. It will take a few minutes for the vSphere Web Client to be initialized.
