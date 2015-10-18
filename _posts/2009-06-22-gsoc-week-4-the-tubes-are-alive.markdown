---
comments: true
date: 2009-06-22 19:20:00
layout: post
slug: gsoc-week-4-the-tubes-are-alive
title: 'GSoC Week 4: The Tubes are Alive!'
wordpress_id: 14
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

Awesome week! Just yesterday, my mentor and I opened up a transatlantic tube and exchanged our Banshee music libraries! Very cool seeing it in action over the Internet. So, I accompished what I wanted to this week and got the data delivering asynchronously without blocking either the producer or consumer's UI. Banshee will display tracks to the user as the download progresses. I've also got playlists coming across too. [Screencast](http://www.youtube.com/watch?v=w31de2K2orA):

**Other happenings:**

 Found a [bug](https://bugs.freedesktop.org/show_bug.cgi?id=22337), confirmed the bug in #telepathy, and reported it.  
  
Also, I found out that Empathy is soon to be ported to Misson Control 5 (MC5). Maybe around GUADEC time. So, this brings a dilemma to my project. See below for a Q and A style explanation.  
  
Q: Why is MC5 important to my SoC project?  
*A: Because the next release of Empathy is going to depend on it, and MC4 is basically being thrown out. No backwards compatibility.*

Q: What is the minimum amount of work required to get this project working with MC5?  
*A:  
1) Port connection detection (ie. ConnectionLocator class) from MC4 API to MC5.  
2) Port presence setting code (ie. Announcer class) from MC4 API to MC5.  
3) Use the Empathy TubeHandler hack (register an object by dbus name __org.gnome.Empathy.DTubeHandler.myservice__) to tell MC5 that Empathy is handling the tube.*

Q: What about the rest of the project's code?  
*A:  
1) Leave the rest of the code as is (with minor tweaks, I'm sure), as I'm pretty sure it will still work.  
2) Port the code to use the org.freedesktop.Telepathy.Client interface MC5 provides.*
 
Q: If we have option 1), then why port anything?  
*A: I am using a bit of a hack, at the moment, for advertising the Banshee music sharing tube service.*
 
The Telepathy API provides a method called SetSelfCapabilities on the ContactCapabilities interface which is kind of weird to work with without MC5. For example, to add a new tube service, the existing services have to be queried, saved, merged with the new service, and then sent to the SetSelfCapabilities method. To remove the new service, the existing services must be queried, saved, our service must be removed from the existing services, and then sent to the method. So, in other words, the method does a replace and not an add/remove operation. MC5 provides a higher level layer that does all this extra work. However, it is quite a bit of work to use that "extra layer." ie. port project code to use the org.freedesktop.Telepathy.Client interface. On the other hand, my hack introduces a race condition where the capabilities could change during the process.  
  
I've [posted](http://lists.freedesktop.org/archives/telepathy/2009-June/003533.html) on the telepathy mailing list about this MC5 stuff and have already received some helpful replies.  
  
So, I'll have to discuss all this with my mentor and decide on our course of action. To add to the TODO list, I may still tweak my playlist provider, I've got some GUI bits to work on and after that I'll probably start playing with file transfers.
