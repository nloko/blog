---
comments: true
date: 2009-09-21 04:40:00
layout: post
slug: mission-control-we-have-lift-off-well-kind-of
title: Mission Control...we have lift off!!! well...kind of
wordpress_id: 22
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

Well, well. The [Telepathy](http://telepathy.freedesktop.org/wiki/) folks have successfully migrated [Empathy to Mission Control 5.](http://www.mail-archive.com/telepathy@lists.freedesktop.org/msg03386.html) While they were probably plugging away, trying to get this migration completed, I was secretly (and sometimes openly) hoping the migration would not get done until after I was done [GSoC](http://code.google.com/soc/).

What do you know. Dreams do come true. GSoC is over.  I survived without having to port to MC5. But, that doesn't mean I don't have anymore work to do. I've already started [porting my Telepathy extension](http://github.com/nloko/banshee/tree/mc5) to the new Mission Control interfaces.

So far, there's nothing exciting to brag about. I've done enough work to prevent the extension from crashing. By using various bits of the new [AccountManager](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.AccountManager.html) and [Account](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Account.html) interfaces, it can find connections and load up who else is online and running the Telepathy extension. What's left? LOTS!

Instead of using the [ContactCapabilities](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Connection.Interface.ContactCapabilities.html) interface to advertise what channels Banshee is going to handle, I need to start using the new method of exporting a DBus object that implements [org.freedesktop.Telepathy.](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Client.html)


[Client](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Client.html) and [org.freedesktop.Telepathy.](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Client.Handler.html)[Client.Handler](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Client.Handler.html). And, I will need to re-work my existing stuff in the extension to manage creating and handling new channels (ie. tubes, file transfers, etc.) using these new interfaces and the [org.freedesktop.Telepathy.](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.ChannelDispatcher.html)


[ChannelDispatcher](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.ChannelDispatcher.html) interface instead of the [Requests](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Connection.Interface.Requests.html) interface. I'm not even sure if I know what all of this means yet. But, I guess figuring it out is part of the fun.

In addition to depending on Mission Control 5, the extension will also have a dependancy on Mono 2.4. Thanks to [packages from directhex](https://launchpad.net/%7Edirecthex/+archive/monoxide), upgrading from 2.0 was a piece of cake. The need for 2.4 is to get around a [bug](https://bugzilla.novell.com/show_bug.cgi?id=481687) that can no longer be avoided.

I wanted to get some more work done this weekend, but I was too busy playing tennis and eating Dim Sum. However, I will devote some more time to this soon. I am setting a goal for myself to get this done before Ubuntu Karmic is released on October 29th. I have two weddings, one in NY and another in Toronto, in October. So, hopefully, I will be sober enough in between to get some things accomplished.





