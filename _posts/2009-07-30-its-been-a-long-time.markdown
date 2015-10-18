---
comments: true
date: 2009-07-30 02:06:00
layout: post
slug: its-been-a-long-time
title: It's been a long time...
wordpress_id: 17
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

...or, at least it feels like it has been. I've been pretty busy hacking away on [my GSoC project](http://github.com/nloko/banshee/tree/gsoc). Speaking of [my GSoC project](http://github.com/nloko/banshee/tree/gsoc), many have asked me "will streaming be a part of it?" And, my answer always was "No, but if I have time, I'll try." Well, it is my pleasure to tell you all that I did have time, I tried, and I succeeded! And, look, I have proof:

[![](http://4.bp.blogspot.com/_d0oLVL7lqBw/SnECczthZQI/AAAAAAAABJM/lKcLQHzhR6o/s400/Screenshot-Drake+Speaks+by+Drake.png)](http://4.bp.blogspot.com/_d0oLVL7lqBw/SnECczthZQI/AAAAAAAABJM/lKcLQHzhR6o/s1600-h/Screenshot-Drake+Speaks+by+Drake.png)

OK. The screenshot is quite boring. But, what it illustrates is a selected instant messaging contact, their library loaded in the track view, and the first song in their library streaming into Banshee.

Now, some may be interested in the technical details of how I accomplished this. In a sad attempt to diagram the flow of what happens in the background, see if this makes any sense:

[![](http://1.bp.blogspot.com/_d0oLVL7lqBw/SnEHNMYBYbI/AAAAAAAABJU/enHw7PzmGiE/s400/Stream+Diagram.png)](http://1.bp.blogspot.com/_d0oLVL7lqBw/SnEHNMYBYbI/AAAAAAAABJU/enHw7PzmGiE/s1600-h/Stream+Diagram.png)

It starts with Contact A. Banshee passes the track URI, something like http://localhost:8080/1234, where 1234 is the trackID in Contact B's Banshee database. Contact A will have the TrackID because they have already downloaded Contact B's music library via a [Telepathy DBus tube](http://telepathy.freedesktop.org/spec.html#org.freedesktop.Telepathy.Channel.Type.DBusTube). Moving on, Banshee, as usual, uses GST (GStreamer) to try to play the track. The URI points to a local proxy which forwards the request over a [Telepathy StreamTube](http://telepathy.freedesktop.org/spec.html#org.freedesktop.Telepathy.Channel.Type.StreamTube) to the Stream server running within Contact B's Banshee. Then, the Stream server looks up where to find the track identified by the trackID on the URI, reads the track from disk, and writes its bytes into a socket connected to an address provided by the StreamTube which points to Contact A's proxy. It finally gets processed by GST and comes through the speakers.

Why a proxy, you may ask? Well, there is a [Mono bug](https://bugzilla.novell.com/show_bug.cgi?id=481687) that prevents me from running the Stream server on an IPv4 socket. Currently, I'm running it on Unix sockets. When using IPv4 sockets with Telepathy Stream tubes, the[ IStreamTube.Accept](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Channel.Type.StreamTube.html#org.freedesktop.Telepathy.Channel.Type.StreamTube.Accept) method returns a variant object. The object must be unboxed into a struct containing the host and port portions of the address. But, the [Mono bug](https://bugzilla.novell.com/show_bug.cgi?id=481687) doesn't let me do that. So, this is how I workaround. When Banshee officially depends on Mono 2.4 (where the bug is supposedly resolved), the proxy can probably go away and the Stream server can plug directly into the Stream tube.

Although slightly less interesting, I should also mention that I've been playing with the [Telepathy Avatars](http://telepathy.freedesktop.org/spec/org.freedesktop.Telepathy.Connection.Interface.Avatars.html) interface. I added an Avatar class to my extension which allows contact's avatars to be downloaded. I put it to use by creating a somewhat half-ass display for the parent container labeled 'Contacts' you see below:

[![](http://3.bp.blogspot.com/_d0oLVL7lqBw/SnEKomz1caI/AAAAAAAABJc/gxUfPE99Uck/s400/Screenshot-Banshee+Media+Player.png)](http://3.bp.blogspot.com/_d0oLVL7lqBw/SnEKomz1caI/AAAAAAAABJc/gxUfPE99Uck/s1600-h/Screenshot-Banshee+Media+Player.png)

As you can imagine, if Avatars are not available, it looks kinda weird with mismatched contacts with Avatars and without. Anyway, this little display looks much better than the big button labeled "Waiting..." that was there before.

So, to sum up all the features of my Telepathy powered extension for Banshee:

* Download your friends' Banshee library metadata and check out what they listen to, their ratings, BPM values, etc.
* View your friends' playlists and export them to disk
* Share what you're listening to with all your instant messaging friends by advertising the track, artist, and album of the currently playing track in Empathy's status message. This can be toggled on / off.
* Download your friends' music; one track at a time or a selection. You can cancel ones in progress, queued, individually or all at once. The sender has the option to cancel all in progress / queued only. Both sender and receiver get a pretty progress bar. File sharing can be toggled on / off.
* Stream your friends' music; no seeking, however. I guess it would make sense to add a toggle option for streaming too.

And, you can do all this without needing to knowing techy details like people's IP address and port numbers. You just have to be connected to a jabber account in Empathy. All contacts running Banshee and the Telepathy extension automagically get loaded into Banshee.

Check out the [README](http://github.com/nloko/banshee/blob/5f6da534f2c083597d9907d4e0b6e4be3563d26c/src/Extensions/Banshee.Telepathy/README) for more information. Feel free to give it a whirl. If you do, I'd love to hear your feedback. I'd be more than happy to help you getting it running and even test it out with you. Be advised, however, that I'm still working out kinks.  Some things are still changing and bugs are getting squashed. But, for the most part, it's in a usuable state.

And...I'm outta here!
