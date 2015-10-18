---
comments: true
date: 2009-11-19 18:45:00
layout: post
slug: banshee-telepathy-extension-0-1-1
title: banshee-telepathy-extension 0.1.1
wordpress_id: 27
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

A day and a few hours later and I'm already releasing [0.1.1](http://github.com/nloko/banshee-telepathy-extension/tarball/0.1.1). Highlights are the following:

* Fix a major bug where the CPU gets maxed out during download of a contact's library
* Prevent 'Too many open files' exception during streaming
* Logging more messages related to streaming
* Fix 'make distcheck' (Fix courtesy of Bertrand Lorentz)
* README updated to reflect a necessary requirement of telepathy-mission-control5 >= 5.3.1
* A few other minor fixes

So, if you're looking to try this out, I suggest you download [this version](http://github.com/nloko/banshee-telepathy-extension/tarball/0.1.1)[.](http://github.com/nloko/banshee-telepathy-extension/tarball/0.1.1)

Testing performed yesterday afternoon and evening confirm that transfer speeds over tubes are highly volatile. Sometimes, it can take up to a few minutes just to offer and accept a tube. And, other times it seems instant. But, more often than not, it's sluggish. If you're using computers on the same network, however, the speeds should be really quick.

Also worth mentioning, [Sandy Armstrong](http://twitter.com/sandyarmstrong) put together some [packages ](http://download.opensuse.org/repositories/home://sanfordarmstrong://banshee-telepathy/openSUSE_11.2/)to help users of openSUSE 11.2 get the dependencies installed.
