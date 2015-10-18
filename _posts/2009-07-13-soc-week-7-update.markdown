---
comments: true
date: 2009-07-13 17:19:00
layout: post
slug: soc-week-7-update
title: SoC Week 7 Update
wordpress_id: 15
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

Time is really flying by. I can't believe we're already halfway finished already! It's been real fun so far. I'm learning a ton, and creating something really cool in the process. :)

For another peek at the coolness I am referring to, take a look at my[ Week 7 Demo](http://www.youtube.com/watch?v=oCyaS-pUZa4) video on [YouTube](http://www.youtube.com/):



As you can see, I have implemented file transfers in my [Banshee extension](http://github.com/nloko/banshee/tree/gsoc).  It has been a little more work than I had anticipated, but the extra work is definitely paying off. I have managed to nicely integrate the transfer(s) progress and give easy access cancel options on an all downloads and per download basis. Of course, it wasn't all my doing. The nice integration was mostly thanks to [pre-existing code](http://git.gnome.org/cgit/banshee/tree/src/Core/Banshee.Services/Banshee.ServiceStack/UserJob.cs) in [Banshee](http://banshee-project.org/).

There are some things that need work, however. I need to give the user some visual feedback of what file(s) are in progress, queued, etc. I have a bit of a start on it, but, when implemented, it's slow. So, this week, I'll be working on that. Some other minor bugs have come up in testing, so I'll also be trying to fix those as well. Debugging can be challenging, as I have DBus, instant messenger, remote connections, threads, etc. to deal with. For the most part, I have been testing quite a bit as I go, but, as most of you know, new annoyances always come up.

I am really dreading the introduction of [MissionControl 5 in Empathy](http://lists.freedesktop.org/archives/telepathy/2009-June/003533.html). It's going to mean some extra work for me to port what I have to the new interface. No word on that for now, however. So, "maybe" it won't happen until after the summer. :)

That's all for now, I guess. I'm really looking forward to the second half of [GSoC](http://code.google.com/soc/) (despite my words in the previous paragraph). On something totally unrelated to my project, I'm really growing tired of my [HTC Touch](http://www.htc.com/www/product/touch/overview.html) cellphone. I think it's time for something new. I'm eyeing the [HTC Magic](http://www.htc.com/www/product/magic/overview.html). The [Android](http://www.android.com/) OS looks wicked, and I think many more awesome things are yet to come. So, when I'm not thinking about SoC, I have an ongoing debate in my brain about whether or not I should buy a new phone.

I've been attempting to make more use of [Twitter](http://twitter.com/) these days, even though most people I know don't use it. I post project updates and also other useless (but sometimes entertaining) drivel. So, feel free to [follow me](http://twitter.com/nloko).
