---
comments: true
date: 2009-11-18 04:55:00
layout: post
slug: banshee-telepathy-extension-0-1-0
title: banshee-telepathy-extension 0.1.0
wordpress_id: 26
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

In an effort to make my Google Summer of Code work more accessible, I've packaged it all up into a [tarball](http://github.com/nloko/banshee-telepathy-extension/tarball/0.1.0) with all the autotools fixins to compile and install for use with your existing Banshee installation.

I felt like some were hesitant to install this because it requires the installation of NDesk.DBus git master. So, I decided to bundle the source into this tarball. It will all get compiled into one Dll, Banshee.Telepathy.dll. This way, everyone can keep their stable versions of NDesk.DBus and still use the extension. When the NDesk guys publish a new release, I will remove the bundled version.

This is largely considered a beta release because it's really only been tested by myself and my mentor. So, please, test away!

Please, read the README before you do anything. There are requirements for this to work properly but are not required to build. Therefore, they aren't checked by the configure script. For easy reference, here are all the requirements:

* Mono >= 2.4.2
* Banshee >= 1.5.1
* Empathy >= 2.27.91
* telepathy-gabble >= 0.9.0

If you're running Ubuntu Karmic, you'll mostly likely have all the requirements except gabble 0.9.0. You can get that [here](http://telepathy.freedesktop.org/releases/telepathy-gabble/). Any of the 0.9.x series will do.

In addition to the requirements in the README, I've made some notes on the issues that I know of. The major one is sluggishness when traffic ends up getting routed through Jabber servers. So, if you end up playing the waiting game, it could be due to [this](https://bugs.freedesktop.org/show_bug.cgi?id=22930). I hope to see some speedier tubes in the future.

If you missed the link for the download above, [here](http://github.com/nloko/banshee-telepathy-extension/tarball/0.1.0) it is again. If you find bugs, it would be awesome if you could file them on the [github issue tracker](http://github.com/nloko/banshee-telepathy-extension/issues). Enjoy!
