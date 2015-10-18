---
comments: true
date: 2012-01-21 07:35:59
layout: post
slug: the-root-of-it-ii
title: Cache Grab
wordpress_id: 435
categories:
- Android
tags:
- Android
- compcache
- Rooting
- Security
---

I came across [this](http://matrixrewriter.com/wiki/tiki-index.php?page=TB+-+Cryptography) today. Whip down to question 11 where is reads...


> I want to use SWAP or COMPCACHE to increase the available RAM on my Android phone. Is that safe ?


The answer there states compcache is _safe _while swap is considered _unsafe_. A closer looks tells a slightly different story, however.

[Compcache](http://code.google.com/p/compcache/) is a system that conserves memory by compressing a portion of it. This portion is readable by the [root](http://en.wikipedia.org/wiki/Rooting_(Android_OS)) user at `/dev/block/ramzswapN`, where `N` is some number. This means that any application running on a device utilizing compcache could have portions of its address space readable from the above mentioned path.

I have a rooted device running custom firmware with compcache installed. So, I tried reading data from the cache after using some apps that contained sensitive information. As I expected, I found that there were pieces of that information in the cache. As with the case [I explored previously](http://nloko.ca/?p=359), passwords and encryption don't help here.

So, would I call compcache any safer than swap? Nope.
