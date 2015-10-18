---
comments: true
date: 2009-10-09 07:00:00
layout: post
slug: mission-control-we-have-lift-off-for-real-this-time
title: Mission Control...we have lift off! (for real this time!)
wordpress_id: 24
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

What do you know. The Telepathy folks have been telling the truth. The [Client.Handler](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Client.Handler.html) interface does work! And, the proof is in an [updated branch](http://github.com/nloko/banshee/tree/mc5) of my Telepathy extension for [Banshee](http://banshee-project.org/).

All functionality has been migrated for compatibility with Mission Control 5. So, the new minimum requirements will be:

* Banshee 1.5
* Mono 2.4
* Empathy 2.27.91
* telepathy-gabble 0.9
* libnesk-dbus git master

I haven't used the [ChannelDispatcher](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.ChannelDispatcher.html) interface, as suggested by the Telepathy folks. I'm still using [Requests](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Connection.Interface.Requests.html) since that route was the least amount of work to get things working with MC5. I don't know if I'll ever change to the ChannelDispatcher interface.

There is still no libndesk-dbus release in sight. So, I haven't put together a nice release with all the autotools fixins. Someday...maybe.

Anyhoo, it's easy enough to pull this [mc5 branch](http://github.com/nloko/banshee/tree/mc5) off github, if you want to try this out.
