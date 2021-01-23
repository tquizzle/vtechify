---
layout: post
title: "Set VMTools Upgrade Policy to Manual"
excerpt: "Small script to set the VMTools policy to manual instead of automatic on power cycle."
tags: [policy, PowerCLI, Upgrade, VMTools]
comments: true
image:
  feature: vSphere6.0.jpg
---


<figure>
	<img src="https://1.bp.blogspot.com/-EEnFTHLxV7A/T0pcaxxsEKI/AAAAAAAAC7k/nYpXbvUx9qA/s1600/tools-policy-0.png">
	<figcaption>Check and upgrade Tools during power cycling</figcaption>
</figure>

By default, many of us probably have our VMs check for new versions of VMTools upon each power cycle. That's usually fine, but in some scenarios it's not. Rather than change the global policy, this script will change just the VMs you want to not upgrade automatically.

{% highlight powershell %}
Get-VM -Name <vmNamesHere> | Get-View | ForEach-Object {
  Write-Output $_.name
  if ($_.config.tools.toolsUpgradePolicy -ne "manual"){
    $vm = Get-VM -Name $_.name
    $spec = New-Object VMware.Vim.VirtualMachineConfigSpec
    $spec.tools = New-Object VMware.Vim.ToolsConfigInfo
    $spec.tools.toolsUpgradePolicy = "manual"
    $_this = Get-View -Id $vm.Id
    $_this.ReconfigVM_Task($spec)
    Write-Output "Completed"
  }
}
{% endhighlight %}