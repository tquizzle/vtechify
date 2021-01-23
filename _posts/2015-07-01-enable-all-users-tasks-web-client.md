---
layout: post
title: "Enable the All Users' Tasks option in the vSphere Web Client"
excerpt: "The vCSA 6.0 doesnt allow you to view All Users' Tasks by default. Let's fix that."
tags: [vCSA, tasks, all users, web client]
comments: true
image:
  feature: vSphere6.0.jpg

---

I've recently deployed several ESXi 5.5 hosts with vCSA 6.0 to test migrating to vSphere 6.0 in my production environment.

I noticed something today that was different than before...you cant view "All Users' Tasks" by default anymore. Weird I thought...but okay. Thankfully, there's [KB 2104914](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2104914) that tells you how to get this done.


## The Fix

> This is a expected behavior.
> 
> To workaround this issue, enable All Users Tasks view in the Recent Tasks section of the vSphere web Client.
> 
> *Note: In a very active environment with many background tasks, performance degradation may occur when this setting is enabled again.*
> 
> To enable All Users Tasks view in the Recent Tasks section of the vSphere Web Client:
> 
> ### For Windows based vCenter Server installation
> 
> 1. Open the webclient.properties file.
> 2. Use a text editor to edit this line: `show.allusers.tasks=false` to read `show.allusers.tasks=true`
> 3. Save the file.
> 4. Restart the vSphere Web Client service using Microsoft Service Manager
> 
> ### For vCenter Server appliance based installation
> 1. Connect to the appliance using SSH and start the bash shell using the command shell.
> 2. Edit the file using the command : `vi /etc/vmware/vsphere-client/webclient.properties`
> 3. Change the parameter from: `show.allusers.tasks=false` to `show.allusers.tasks=true`
> 4. Save and exit vi mode using `:wq`.
> 5. Restart the vSphere Web Client service using this command: `service vsphere-client restart`

There, all done. Now once the vCenter Web Client Service starts back up, you'll be able to view the "All Users' Tasks" like before.
