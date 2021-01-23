---
layout: post
title: "vMotion fails with error 'Failed to create journal file...'"
excerpt: "How to fix the nuance of Failed to create journal file..."
tags: [file system, SNMP, trap]
comments: true
image:
  feature: vSphere6.0.jpg
---


A few days ago an issue arose that caused me to not be able to vMotion to and from a particular host. Not only would typical vMotions not work, but storage vMotion would also fail at around 33%. Each of these errors hinted to the file system being full because the host could not update or create log or journal files.

After poking around, I found that the /var/spool/snmp directory had thousands, upon thousands of files in it. SNMPd was running and the host had all the valid settings necessary for it to be able to send traps to the SNMP server, yet it was queueing them up in this directory.

Deleting them solved the issue, but only temporarily…

I then found [KB 2040707](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2040707) which explains that this issue is a known issue affecting ESXi 5.1.

Here's the work around:

1. Find out if your directory is full of .trp files
{% highlight powershell %}
ls /var/spool/snmp | wc -l
{% endhighlight %}
2. Delete said .trp files
3. Backup the snmp.xml file
{% highlight powershell %}
mv /etc/vmware/snmp.xml /etc/vmware/snmp.xml.bak
{% endhighlight %}
4. Create a new snmp.xml file and place it in the /etc/vmware directory
Below is the contents of the file needed:
{% highlight powershell %}
<?xml version="1.0" encoding="ISO-8859-1"?>
<config>
<snmpSettings><enable>false</enable><port>161</port><syscontact></syscontact><syslocation></syslocation>
<EnvEventSource>indications</EnvEventSource><communities></communities><loglevel>info</loglevel><authProtocol></authProtocol><privProtocol></privProtocol></snmpSettings>
</config>
{% endhighlight %}
5. Reconfigure SNMP on the host by running the command:
{% highlight powershell %}
esxcli system snmp set --enable=true
{% endhighlight %}
