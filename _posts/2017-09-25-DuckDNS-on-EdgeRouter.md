---
layout: post
title: "DuckDNS on EdgeRouter"
excerpt: "Setting up DuckDNS as a Dynamic DNS provider is easier and harder than expected."
tags: [EdgeRouter, EdgeMax, DNS, DuckDNS, Dynamic DNS, router]
comments: true
#image:
#  feature: vSphere6.0.jpg

---

[Logan Marchione](https://loganmarchione.com) has a great series of articles about the Ubiquiti EdgeRouter. I was interested in particular to setting up DuckDNS as a dynamic DNS provider. He covered that well using the command line.

I'm not sure why I couldn't get it to work, but for some reason a handful of the commands were generating errors in my configuration. I set out to figure it out using the GUI. It wasn't hard, just took looking at [Logan's article](https://loganmarchione.com/2017/04/duckdns-on-edgerouter/) and dissecting it a bit.

PreRequisite: You must sign up for [DuckDNS service](https://www.duckdns.org/). Get logged in and create your hostname and create your token.

1. Go to Dynamic DNS settings page in the GUI of your EdgeRouter.
  * Services -> DNS
2. Create a new DDNS Interface and choose your WAN interface. Mine is eth2.
3. Choose Custom as the service and give it a friendly name
4. Put in your hostname without the duckdns.org in hostname
5. Login username is 'nouser' / Password is your account token.
6. Protocol is dyndns2
7. Server is www.duckdns.org

Apply that change and you should be in business.

![EdgeRouter DDNS]({{ site.url }}/images/edgerouter-dynamic-dns.png)


You can always see the status by opening up console to your router and issuing the following command:

~~~ bash
show dns dynamic status
~~~

Output:
~~~ bash
interface    : eth2
ip address   : X.X.X.X
host-name    : MyHostname
last update  : Sun Sep 24 17:57:40 2017
update-status: good
~~~

Now you're all set.
