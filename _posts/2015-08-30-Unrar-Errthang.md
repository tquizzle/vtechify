---
layout: post
title: "Exract All RAR Files"
excerpt: "Sometimes, you just don't want to keep typing the same one or two-liners. Sometimes it's just easier to whip up a quick script."
tags: [unrar, extract, formatting, format]
comments: true

---

![Unrar]({{ site.url }}/uploads/2015/08/unrar-256x256.png)
{: .image-pull-right}
Sometimes I'm lazy. 
Sometimes I try to think of better ways to do things even if there exists a perfect way to do it already.

Every once-in-a-while there is a time when I need to so some mass unraring. I might have a ton of files possibly even rar'd up differently. Some of them might be multi-part RARs with part1.rar, part01.rar, part001.rar or just .rar.
I wanted something to take care of all of them regardless of the style they were compressed.

So I came up with this. I think this will work.

**Adjust your "-maxdepth" as necessary.**
<br clear="right" />
<script src="https://gist.github.com/tquizzle/ef82a7e9f4e008fc35c8.js"></script>
