---
comments: true
date: 2009-05-06 05:21:00
layout: post
slug: tubing-anyone
title: Tubing anyone?
wordpress_id: 10
categories:
- Summer of Code
tags:
- GNOME
- Telepathy
---

Telepathy tubing that is. And, call me crazy, but today's tubing adventure was quite fun. I spent most of today working on a test using C# to access a remote D-Bus interface over a D-Bus tube. The [code](http://github.com/nloko/telepathy-sharp/blob/facdc293192f9c8d9282977a9db8a97ce16ee385/tests/DTubeTest.cs) for this test actually tests a lot more than just D-Bus tubes, as there a number of things that need to happen before the tube can get setup and used. Also, the API has been changing faster than most of the examples out there can keep up. So, this test required some experimenting with the newer [Requests interface](http://telepathy.freedesktop.org/spec.html#org.freedesktop.Telepathy.Connection.Interface.Requests) and [DBusTube type channel](http://telepathy.freedesktop.org/spec.html#org.freedesktop.Telepathy.Channel.Type.DBusTube.DRAFT). It was a great exercise to learn how well C# and Telepathy can play together. With the help of the [bindings](http://github.com/nloko/telepathy-sharp/tree/master) I've put together, the verdict is: so far so good.   
  
The test isn't complete, but the exciting stuff is all there. I'll probably finish that up tomorrow and move on to other interesting things related to my [SoC project for Banshee](http://nlokos.blogspot.com/2009/04/big-news.html). I've got a Google document going full of design details and other things I want to note before I forget them forever. I think a list of test cases will be good to start thinking about too. The plan is to have all this deep thought out of the way before our official coding start date.   
  
But, before any more thinking, I think it's time to tear myself away from this computer and go do something completely mindless.
