---
layout: post
title: "Clearing out the /boot partition on Ubuntu Server"
excerpt: "Don't let that /boot fill up, Yo!"
tags: [linux, Ubuntu, file system]
comments: true
---

Recently I had an issue where I could no longer update packages. The system was responding normally, but after digging around, I found that the /boot partition was 100% full.

{% highlight bash %}
df -h
{% endhighlight %}

After digging around on Google for a while, I found this little gem.

{% highlight bash %}
dpkg --get-selections|grep 'linux-image*'|awk '{print $1}'|egrep -v "linux-image-$(uname -r)|linux-image-generic" |while read n;do apt-get -y remove $n;done
{% endhighlight %}
