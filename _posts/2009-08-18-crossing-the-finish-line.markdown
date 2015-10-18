---
comments: true
date: 2009-08-18 21:09:00
layout: post
slug: crossing-the-finish-line
title: Crossing the Finish Line
wordpress_id: 19
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Summer of Code
- Telepathy
---

![](http://lh3.ggpht.com/_d0oLVL7lqBw/SotANkoFiRI/AAAAAAAABKs/7D-og6fbz6k/s400/song_playing.png)

Well, the final week of [GSoC](http://code.google.com/soc/) has come to an end. The final surveys are being submitted; the final status reports have been sent to [gnome-soc](http://mail.gnome.org/archives/gnome-soc-list/2009-August/thread.html). It is the end of an era. Alright, I'm being a little over dramatic. But, it has definitely been a fun summer. Hacking on an awesome project like [Banshee](http://banshee-project.org/) was a great way to spend the last few months. The above screenshot gives a good look at the fruits of my labour. But, to learn more, please read on... 

**Highlights for The Final Week**

* Gave my "Share Currently Playing" feature a smarter brain. It will now reset to display the user's presence on Empathy if playback is paused. Announcements then restart when playback is resumed. Also, the announcement is reset to display the user's presence when Banshee quits.
* Submitted 2 patches for review: 
* A [base web server class](http://bugzilla.gnome.org/show_bug.cgi?id=591481) that gets implemented by my extension and DAAP
* [Enable seeking](http://bugzilla.gnome.org/show_bug.cgi?id=547719) in DAAP streams
* Disable 'Download Track' option on the client side if the user serving tracks has 'Allow Downloads' disabled.
* Improved downloading of library metadata. User feedback feels much faster and the UI is updated more often.
* Some improvements in the file transfer logic that prevent sluggishness when a lot of transfers are in progress and/or queued.
* Lots of tests, fixes, tweaks, etc.

**So, What The Heck Is This Thing, Anyway?**

Well, what I have created is a [Telepathy](http://telepathy.freedesktop.org/wiki/) based extension for Banshee. Using the[ Telepathy API](http://telepathy.freedesktop.org/spec.html), the extension provides the following
features:

* Download your friends' Banshee library metadata and check out what they  listen to, their ratings, BPM values, etc.

![](http://lh4.ggpht.com/_d0oLVL7lqBw/Sos_FSm7xzI/AAAAAAAABKk/X6ftXxTQQto/s400/Contact%20Request.png)

* View your friends' playlists and export them to disk
* Share what you're listening to with all your instant messaging friends by advertising the track, artist, and album of the currently playing track in Empathy's status message. This can be toggled on / off.

![](http://lh3.ggpht.com/_d0oLVL7lqBw/SotroMoH_PI/AAAAAAAABMA/aCDTx-fmB0s/s800/empathy.png)

* Download your friends' music one track at a time or with a selection. You can cancel, individually or all at once, downloads that are queued and/or in progress. The sender has the option to cancel all only. Both sender and  receiver get a progress bar. File sharing can be toggled on / off.

![](http://lh4.ggpht.com/_d0oLVL7lqBw/Sos4IwSh0JI/AAAAAAAABKc/JKqzZF1S2KY/s800/contacts_menu.png)

* Stream your friends' music. You can pause, you can seek, you can skip, you can even use the play queue. Streaming can be toggled on / off, as shown in the above screenshot.

![](http://lh4.ggpht.com/_d0oLVL7lqBw/SotroaGzyxI/AAAAAAAABME/lRTkYFUYWKk/s800/streaming.png)

**Requirements**

* telepathy-gabble >= [0.7.28](http://telepathy.freedesktop.org/releases/telepathy-gabble/telepathy-gabble-0.7.28.tar.gz)
* banshee = [1.5.1](http://download.banshee-project.org/banshee/unstable/1.5.0/banshee-1-1.5.0.tar.bz2), [GIT master](http://git.gnome.org/cgit/banshee/) recommended
* empathy >= [2.26.1](http://ftp.acc.umu.se/pub/GNOME/sources/empathy/2.26/empathy-2.26.1.tar.bz2), [latest release](http://ftp.acc.umu.se/pub/GNOME/sources/empathy/2.27/empathy-2.27.5.tar.bz2) recommended
* libndesk-dbus = [git master ](http://gitweb.ndesk.org/?p=dbus-sharp)

The dependency on NDesk.DBus git master is not ideal. But, it is necessary for this to work. The main thing is that GIT master gives support for out parameters. I've been using it the entire summer without any problems.

**Where to get it**

It's being [hosted on Github](http://github.com/nloko/banshee/tree/gsoc) as a personal branch of the entire Banshee source. It was merged with master very recently, so it is very current with Banshee development. I've also package this up as a [standalone extension](http://github.com/nloko/banshee-telepathy-extension/tree/master) to make it easier for users to install on top of their existing Banshee installations. The autotools logic needs some polish, but don't let that stop you from using it. The caveats to be aware of with the standalone installer are that the installation requirements are verified, but the versions of the requirements are not. So, please be sure you have the minimum versions mentioned above before installing. See the [README](http://github.com/nloko/banshee-telepathy-extension/blob/afafa4eda4ef6e447e473a4994c28d97c87131f5/README) for more information.

To be safe, please backup your Db first:
cp ~/.config/banshee-1/banshee.db ..............

Don't worry too much. I have not damaged mine over the entire course of SoC.

**Known Issues**

I have written in more detail about known issues in my [README](http://github.com/nloko/banshee/blob/02189ddfe94fc29c82de1890547e6380a1dbb6c3/src/Extensions/Banshee.Telepathy/README). However, I will briefly summarized the major ones here:

* Transfer speeds are highly dependent on the Telepathy framework's ability to establish a P2P connection. If traffic goes through Jabber servers, be prepared for a highly sluggish experience. In testing, use on a LAN is very quick.See [https://bugs.freedesktop.org/show_bug.cgi?id=22930](https://bugs.freedesktop.org/show_bug.cgi?id=22930)
* The Empathy trayicon will display a blinking lightning bolt when there is a file transfer. Clicking it will display a dialog box for accepting/rejecting the transfer. Using this will cause unpredictable results. Telepathy Mission Control 5 will allow this to be suppressed. If you pop up the dialog by accident, just click the 'X' to close it and all will be good.
* This extension will overwrite any existing Telepathy capabilities being advertised. This is due to the ContactCapabilities.SetSelfCapabilities interface performing a replace operation and not an append. I chose not to develop a workaround for this, as Mission Control 5 will allow this process to work correctly.

**The Future**

Once Empathy migrates to Mission Control 5 (latest release currently uses 4.67), the extension will have to be brought up to date. This will not be a trivial thing. It will be some work, but nothing to really cry about. I would love for the project to someday be merged into the Banshee source for distribution as a default extension. To make that a possibility, I intend to keep it current and stable. In fact, I already have some ideas for new features for the Telepathy extension.

It's been an awesome summer. So awesome, in fact, that I am really looking forward to contributing more, and more to Banshee, GNOME, and other FOSS projects. And, before I forget, my mentor, Bertrand Lorentz, deserves a special thanks for all the help and testing over that last few months. I owe you a beer...at least!
