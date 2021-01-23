---
layout: post
title: "PowerCLI on OSX"
excerpt: "Several posts are out there talking about how to do this, but I figured I'd put my post together of what I did to get this new functionality in OSX."
tags: [PowerShell, PowerCLI, OSX, Shell]
comments: true
image:
  feature: vSphere6.0.jpg

---

There have been a few posts out there talking about how to install PowerCLI on OSX so I figured I'd just make my own post about what I did.


### HomeBrew

You should already have [this](https://brew.sh/). If not, find out about it and make it happen.

Now you need to add [HomeBrew-Cask](https://caskroom.github.io/) so you can get more goodies from HomeBrew.

{% highlight bash %}
brew tap caskroom/cask
{% endhighlight %}

Now install PowerShell

{% highlight bash %}
brew cask install powershell
{% endhighlight %}

Does it work?

{% highlight bash %}
pwsh
{% endhighlight %}

### PowerCLI

Now we can easily install PowerCLI.

{% highlight powershell %}
Install-Module -Name VMware.PowerCLI -Scope CurrentUser
{% endhighlight %}


#### Default certificate handling

Now we get errors when connecting to a vCenter with self-signed certificates.
We'll have to fix that!

{% highlight powershell %}
Set-PowerCLIConfiguration -InvalidCertificateAction Ignore
{% endhighlight %}



### More Info:

* Duncan Epping - http://www.yellow-bricks.com/2018/03/01/powercli-for-osx-is-out/
* Michael White - https://notesfrommwhite.net/2018/02/28/installing-powershell-powercli-on-a-mac/
* Kyle Ruddy - https://blogs.vmware.com/PowerCLI/2018/02/powercli-10.html
