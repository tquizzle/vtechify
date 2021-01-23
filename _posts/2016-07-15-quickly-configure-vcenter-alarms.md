---
layout: post
title: "Quickly Configure vCenter Alarms with PowerCLI"
excerpt: "When you need to quickly make some modifications to vCenter alarms, check out some of these little snippets."
tags: [vCenter, alarms, snippets, PowerCLI]
comments: true
image:
  feature: vSphere6.0.jpg

---
I found the below snippets on [VirtIRL](http://virtirl.com/?p=196).

This configures all vCenter alarms to send an email:
{% highlight powershell %}
Get-AlarmDefinition | New-AlarmAction -Email -To 'admin@example.com'
{% endhighlight %}


Now you can create an alarm trigger to send an email when the monitored item changes from green to yellow as well. The default alarm action automatically creates the alert for yellow to red (above example).
{% highlight powershell %}
Get-AlarmDefinition | Get-AlarmAction -ActionType SendEmail | where-object {$_.To -like 'admin@example.com'} | New-AlarmActionTrigger -StartStatus 'Green' -EndStatus 'Yellow'
{% endhighlight %}

To add other transitions (red to yellow, yellow to green) you can just change the **-StartStatus** and **-EndStatus** to the necessary values.
{: .notice}

To see all Alarms configured to send to a certain email address along with triggers:
{% highlight powershell %}
Get-AlarmDefinition | Get-AlarmAction -ActionType SendEmail | Where-Object {$_.To -like 'admin@example.com'} | Select AlarmDefinition,To,Trigger
{% endhighlight %}

To remove all SendEmail AlarmActions for a particular email address:
{% highlight powershell %}
Get-AlarmDefinition | Get-AlarmAction -ActionType SendEmail | where-object {$_.To -like 'admin@example.com'} | Remove-AlarmAction
{% endhighlight %}
