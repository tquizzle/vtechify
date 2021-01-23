---
layout: post
title: "vCSA gives error trying to login - cannot get user info"
excerpt: "When using Windows session authentication you get an error that says 'Cannot get user info'. That's not cool, so here's how to fix that."
tags: [vcenter, vcsa, appliance, user, info]
comments: true
image:
  feature: vSphere6.0.jpg

---

After deploying the vCSA 6.0 in my development lab I was running into some issues logging in. I kept getting an error "A General System error occurred: Cannot get user info".

I found the solution over at the [VMware KB site](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2050701).


### Symptom



- Cannot log in to the vCenter Server Appliance (VCSA) as vSphere Client users by using the Use Windows session credentials option
- Logging in to vCenter Server Appliance (VCSA) using the Use Windows session credentials option fails
- You see the error:

    A General System error occurred: Cannot get user info

- In the `vpxd` logs on the vCSA you see entries similar to:

~~~ bash

<YYYY-MM-DD>T<TIME>+02:00 [7F1C10CCC700 error 'GSSAPI' opID=CEAEA705-00000004-2d] Cannot get user info for XXXX\YYYY. Possible NSS configuration problem.
<YYYY-MM-DD>T<TIME>+02:00 [7F1C10CCC700 info 'commonvpxLro' opID=CEAEA705-00000004-2d] [VpxLRO] -- FINISH task-internal-9727699 -- -- vim.SessionManager.loginBySSPI
<YYYY-MM-DD>T<TIME>+02:00 [7F1C10CCC700 info 'Default' opID=CEAEA705-00000004-2d] [VpxLRO] -- ERROR task-internal-9727699 vim.SessionManager.loginBySSPI: vmodl.fault.SystemError:
Result:
(vmodl.fault.SystemError) {
dynamicType = <unset>,
faultCause = (vmodl.MethodFault) null,
reason = "Cannot get user info",
msg = "",
}
Args:

~~~


### Resolution

You can work around it by just typing your credentials in, but then what's the use with installing the plugin if you cant use your Windows credentials?


To resolve this issue:

- Log in to vCenter Server Appliance as the root user.
  - For vCenter Server Appliance 6.0:
    - To enable the Bash shell, run the `shell.set --enabled true` command.
    - Run the shell command to start the Bash shell and log in.
- Open the /etc/nsswitch.conf file using vi
  - `vi /etc/nsswitch.conf`  
  - Locate the `passwd: compat ato` entry and replace it with the `passwd: compat ato lsass`.


Note: Remove lsass from the line if it is currently displayed.
Restart the services using /etc/init.d/vmware-vpxd restart.
{: .notice}

- Restart vpxd by running this command: `/etc/init.d/vmware-vpxd restart`



