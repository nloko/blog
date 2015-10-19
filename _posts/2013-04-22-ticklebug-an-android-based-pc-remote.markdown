---
layout: post
title: "Ticklebug"
date: 2013-04-22 22:57
comments: true
categories:
- Android
- Programming 
---

I created [Ticklebug](http://ticklebugapp.ca) to solve a problem for myself, and I've decided to [share it](https://play.google.com/store/apps/details?id=com.nloko.android.ticklebug).

Ticklebug was born as result of [saying goodbye to cable subscription fees](http://lifehacker.com/5667680/ditching-cable-for-the-web-how-much-can-you-save-buying-renting-or-streaming-tv) in our home.
Bye, bye fees. Bye, bye cablebox. And, Hello, [HTPC](http://en.wikipedia.org/wiki/Home_theater_PC)!

## The Need

Obviously, I wasn't going to be walking up to the television set to fiddle around with a keyboard and
mouse everytime I wanted to watch something. That would be way too much exercise for something that's
really supposed to involve as little exercise as possible. Initially, my solution for this problem was
one of those [wireless keyboards with an integrated trackball](http://www.amazon.com/Multimedia-Keyboard-Trackball-Wireless-GKM561R/dp/B002H0BOBA).
Don't get me wrong, the combination is pretty awesome. After awhile, though, I noticed that I was playing with
my phone a lot of the time while watching TV. So, I thought it'd be great if I could use my phone as a remote
control!

I began searching for and trying various Android apps for remote controlling my HTPC. However, I wasn't
completely happy with any of them. In my ideal remote control app, I wanted the following features:

1. A maximum surface, blank canvas that acts like a **touchpad**, very similar to how laptop touchpads behave.
1. **Mac and Windows** support, as I use both regularly.
1. **Voice commands** so I can tell my computer what I want it to do.
1. **Zoom!** Because, as great as high-def is, sometimes things are just hard to read.

## Features

Ticklebug has a [long list of features](https://play.google.com/store/apps/details?id=com.nloko.android.ticklebug),
so I won't go over everything. What I will do, though, is I'll go over the above list and tell you a little about how Ticklebug handles each.

### Touchpad

Ticklebug maximizes your mobile device's screen space keeping it uncluttered at all times. There are a very 
limited number of buttons. To interact, touches, drags, and taps are used liberally. To make Ticklebug super easy to use, the gestures are very familiar:

- Drag a finger to move the mouse pointer
- Drag two fingers to scroll within windows
- Long-press a finger and drag to move or resize windows
- Single-tap to left click and double-finger-tap to right click
- Swipe left or right to navigate back or forward, respectively, when web browsing

### Cross-platform

I use a Macbook most of the time. But, my HTPC runs Windows 8. I'm a faithful subscriber to [Netflix](http://www.netflix.com),
and running Windows just makes using the service much [easier than using another operating system](http://www.jeremymorgan.com/tutorials/linux/how-to-netflix-ubuntu-linux/).
Thus, I needed Ticklebug to be cross-platform to get the most out of it. As a result, there are [desktop applications](http://ticklebugapp.ca/downloads) for both Mac and Windows.

### Voice Commands

What's cooler than speaking instructions to your computer? Nothing! So, I gave Ticklebug the smarts to understand a few commands:

- Say *Google* followed by some search words and your default browser will load with the search terms ready
to go in Google's search bar.
- Say *Open* followed by some site name and your default browser will load it. For example, say *open youtube dot com*,
and `http://youtube.com` wlll load.

And, in the [paid version of Ticklebug](https://play.google.com/store/apps/details?id=com.nloko.android.ticklebug.pro):

- Say *Start* followed by the name of some executable file, and your computer will run it. For example, say *start notepad*,
and Notepad will start.

What's great about the last command is that you can create your own voice commands to do just about anything! For example, on Windows 8,
[Netflix](http://www.netflix.com) has some [weird, wild, hidden file name](http://www.itsjustwhatever.com/2012/10/28/launch-windows-8-metro-apps-from-a-desktop-shortcut-or-command-line) making it difficult to launch using a voice command.
However, the application will run if you type `netflix://` into a browser. We can use this piece of information to create a custom voice command.

On my computer, I've created a [script](http://en.wikipedia.org/wiki/Batch_file) named `netflix.bat` and saved it in a directory
that's specified in my [PATH environment variable](http://en.wikipedia.org/wiki/PATH_%28variable%29). The contents look like the following:

~~~ 
:: Launch Netflix app on Windows 8
cmd /c "start netflix://"
exit 0
~~~ 

Now, I can say *start Netflix* to launch the app without typing a thing!

### Pinch-to-zoom

Again, using Netflix as the example, those little video thunbnails in the Windows 8 app are pretty hard to read most of the time. I really
wanted to be able to zoom in the way you can when using your phone's web browser. So, in Ticklebug, you can move two
fingers apart to zoom in and move two fingers together to zoom out. And, this gesture can be used within any application, including
the desktop.

## In Stores Now!

<img src="https://dl.dropbox.com/u/6578423/gnexus.png" alt="Ticklebug for Android" width="400" />
{:.center}


If you have an Android device running Android 4.0 or higher, [give Ticklebug a try!](https://play.google.com/store/apps/details?id=com.nloko.android.ticklebug)
