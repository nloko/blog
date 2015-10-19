---
comments: true
date: 2012-05-26 06:40:36
layout: post
slug: consoleme
title: consoleme
wordpress_id: 465
categories:
- iOS
- Objective-C
- Programming
tags:
- Console
- iOS
- iPad
- iPhone
- Log
- Objective-C
---

Let's face it. Geeks like logs. Scrolling text, line by line, running programs spewing out meaningful information by the second. Comforting, isn't it? Don't you just wanna `tail -f /var/log/syslog` right now!?!

## Output. Need More Output!

If you're like me, when using your magical iOS devices, you don't always feel quite at home. There's something missing: the system log! You can't view it! Well, [not all that easily](http://superuser.com/a/15860), anyway.

## Solution? consoleme!

We all like easy, even developers like me. Enter, consoleme! An app I wrote to allow you to view your iOS device's system log right on your device without hooking it up to your Mac.

Some things it does:
	
* Persistent log history
* E-mail to your buddies
* On-demand, instant refresh

It's also pretty easy to use. A recent snapshot of the log is loaded when the app starts. Once the app has started, simply tap anywhere on the screen to perform additional actions. And, that is all there is to it!

## Screenshots

I know you like pictures. So, here are some pictures...

![](https://lh3.googleusercontent.com/-dBZbLpUaDHU/T8BuSA_ORRI/AAAAAAAAB_4/7w9h_THHjF8/s673/Screen+Shot+2012-05-10+at+11.53.15+PM.png "Running on an iPad. Loads and loads of system log data. ["I don't even see the code."](http://www.youtube.com/watch?v=3vAnuBtyEYE&feature=player_detailpage#t=9s)")
{:.center}

![](https://lh4.googleusercontent.com/-mjr18VR5NXA/T8BuTgftivI/AAAAAAAACAI/4OGt5_ZJ4CE/s545/Screen+Shot+2012-05-10+at+11.54.26+PM.png "Loading on an iPhone")
{:.center}

![](https://lh3.googleusercontent.com/-mN3R6akdwXk/T8BuTX45e0I/AAAAAAAACAA/uSMWHvAbz5E/s545/Screen+Shot+2012-05-10+at+11.54.12+PM.png "As you can see, the design is very minimal yet self-explanatory")
{:.center}

## You Want It? You Got It!

It's not groundbreaking stuff, I know. There are other apps. But, this one is free and it's available, source code and all, on [github](https://github.com/nloko/consoleme). It depends on my other project, [NLOSyslog](https://github.com/nloko/NLOSyslog), which has been included in the consoleme project. Both projects are in their infancy. Thus, there are no official releases. However, everyone is more than welcome to the source or, even better, send me pull requests!
