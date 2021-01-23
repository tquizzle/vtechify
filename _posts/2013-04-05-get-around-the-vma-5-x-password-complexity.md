---
layout: post
title: "Get Around the vMA 5.x Password Complexity"
excerpt: "Where there's a will, there's a way."
tags: [Password Complexity, vMA, Appliances]
comments: true
image:
  feature: vSphere6.0.jpg
---

<figure>
	<img src="http://i2.wp.com/v-reality.info/wp-content/uploads/2011/08/image1.png">
	<figcaption>Ridiculous password complexity</figcaption>
</figure>

When deploying the latest vMA appliance I was hit with a highly restrictive password complexity requirement from VMware. I could not let this get the best of me.

Thanks to [Tomi Hakala](http://v-reality.info/2011/08/how-to-fix-vma-5-0-password-complexity-issue/), I didn’t have to.


1. Set valid password for vi-admin, for example Qazx123!# should do
2. Login to vMA shell as vi-admin
3. Elevate session as root with “sudo –s”
4. Run “pam-config –d –-cracklib”, note double dashes on front of cracklib
5. Exit root shell with “exit”
6. Change vi-admin password with “passwd” to your liking

Above pam-config command disables cracklib in vMA PAM (pluggable authentication module) configuration, cracklib is a PAM library which is used to enforce Linux, and it this case vMA account password strength.
{: .notice}
