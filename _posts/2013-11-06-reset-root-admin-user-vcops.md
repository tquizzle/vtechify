---
layout: post
title: "Reset the root or admin user in vCOps"
excerpt: "When deploying, you have to change the root and admin passwords. What happens if you can't remember what you set it as? Here I explain how you can reset."
tags: [Unsupported, vCOps]
comments: true
image:
  feature: vSphere6.0.jpg
---

This also works in vCenter Infrastructure Navigator
{: .notice}

When you log into each of these appliances the first time, it requires you to change the password. What happens if you can’t remember what you set it as? How can you log in to change the users if you don’t know the password to do so?

I found myself in this very scenario recently and sought out to resolve this. After searching and searching I found this.

To reset the root user password in the vCenter Operations or Infrastructure Navigator virtual appliance console:

1. Boot the virtual appliance and navigate to the console for the virtual machine in the vSphere Client.
2. Click in the console and press any key to display the GRUB menu.
Note: The GRUB prompt remains on screen for 7 seconds before it starts the boot sequence.
3. On the GRUB menu, select SUSE Linux Enterprise Server for VMware.
4. Type e to edit the line. A list of items in the GRUB configuration file appears.
5. Select the line that starts with kernel and type e to edit the line.
6. At the end of the line, press the spacebar and type init=/bin/sh.
7. Press Enter to exit edit mode.
8. On the GRUB screen, type b to boot into single-user mode.
The virtual appliance boots in single-user mode.
9. To change the root user password, type passwd root and follow the on-screen prompts.
10. To restart the virtual appliance, type reboot and press Enter.

When the virtual appliance restarts, you can log in using the new password.
{: .notice}