---
comments: true
date: 2009-08-06 17:43:00
layout: post
slug: learning-new-things-all-the-time
title: Learning new things all the time
wordpress_id: 18
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Streaming
- Telepathy
---

This morning, I was able to enable seeking when streaming a contact's library in my[ Telepathy extension for Banshee](http://github.com/nloko/banshee/tree/gsoc).  For the longest time, I figured it would just work. Of course, it's not that easy. So, last night I decided to do some googling. In turns out that, when streaming via HTTP, to request a skip, an HTTP [Range header](http://www.freesoft.org/CIE/RFC/2068/198.htm) gets sent within the body of the request. So, the full HTTP request to skip to some point in a stream may look something like the following, which I captured from [totem](http://projects.gnome.org/totem/) (the key bit is in bold):


> GET / HTTP/1.1
Host: localhost:8080
Connection: close
icy-metadata: 1
transferMode.dlna.org: Streaming
Range: bytes=2602384-
User-Agent: GStreamer souphttpsrc libsoup/2.26.0


To identify to the client making the request that seeking is supported, a[ 206 Partial Content status code](http://www.freesoft.org/CIE/RFC/2068/81.htm) must be sent back, instead of the usual 200 OK. In addition to this, a [Content-Range header field](http://www.freesoft.org/CIE/RFC/2068/178.htm) must be included indicating where the partial content starts and ends. Therefore, the [Content-length header](http://www.freesoft.org/CIE/RFC/2068/175.htm) must also be augmented to account for the size of the partial content being sent.

So, to enable seeking in my stream server within my Banshee extension, all I had to do was send the appropriate HTTP status code, headers, and partial stream of music.

Skip, skip, skip to my loo.
