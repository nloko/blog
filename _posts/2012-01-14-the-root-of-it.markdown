---
comments: true
date: 2012-01-14 17:15:11
layout: post
slug: the-root-of-it
title: The Root of It
wordpress_id: 359
categories:
- Android
tags:
- Android
- Rooting
- Security
---

You've heard of Android. But, what do you know about Rooting? What the heck is that you might ask? Custom community developed [ROMs](http://forum.xda-developers.com/forumdisplay.php?f=565) are all the craze these days and in order to install them, you'll need to perform a process called _[Rooting](http://en.wikipedia.org/wiki/Rooting_(Android_OS))_. This gives you complete, no holds barred access to your device. Sounds great, right? But, consider what would happen if your precious device were to fall into the wrong hands? Here is an example of what could go wrong.

Using the [Android SDK](http://developer.android.com/guide/developing/tools/adb.html), with your device wired in via USB, you can remote shell into it via `adb shell`. From here, you can poke around and find all sorts of things. Issuing `ps` within the shell will display output similar to the following:




    
    USER     PID   PPID  VSIZE  RSS     WCHAN    PC         NAME
    system    497   122   114564 18008 ffffffff afd0ee3c S com.android.settings
    app_16    522   122   117952 13276 ffffffff afd0ee3c S com.google.android.voicesearch
    root      539   2     0      0     c006a118 00000000 S tiwlan_wifi_wq
    wifi      543   1     3112   752   ffffffff afd0deb4 S /system/bin/wpa_supplicant
    app_10    711   122   109676 14248 ffffffff afd0ee3c S com.android.providers.calendar
    app_57    764   122   0      0     ffffffff 00000000 Z droid.apps.docs
    app_17    816   122   119136 23252 ffffffff afd0ee3c S com.android.vending
    dhcp      875   1     936    372   c00d6198 afd0ec0c S /system/bin/dhcpcd
    app_14    932   122   105392 12868 ffffffff afd0ee3c S com.android.defcontainer
    app_30    962   122   105400 12272 ffffffff afd0ee3c S com.svox.pico
    app_43    976   122   135648 22348 ffffffff afd0ee3c S com.google.android.apps.maps
    app_42    996   122   105376 12216 ffffffff afd0ee3c S com.android.vending.updater




  


This is a listing of all running processes on the device. Each process has a unique identifier called a _PID_. With root access, we can actually dump process memory (live application data) to a file by sending the process the `SIGUSR1` [kill signal](http://en.wikipedia.org/wiki/Kill_(command)). The generated file is called a [heap dump](http://blogs.oracle.com/alanb/entry/heap_dumps_are_back_with) and can be created by issuing `kill -10 _pid_` in the shell.

You'll know it was successful because you'll see something similar to the below in the log:




    
    I/dalvikvm( 1003): threadid=3: reacting to signal 10
    I/dalvikvm( 1003): SIGUSR1 forcing GC and HPROF dump
    I/dalvikvm( 1003): hprof: dumping VM heap to "/data/misc/heap-dump-tm1326509736-pid1003.hprof-hptemp".
    I/dalvikvm( 1003): hprof: dumping heap strings to "/data/misc/heap-dump-tm1326509736-pid1003.hprof".
    I/dalvikvm( 1003): hprof: heap dump completed, temp file removed
    D/dalvikvm( 1003): GC_HPROF_DUMP_HEAP freed 1461 objects / 141080 bytes in 5951ms




  


Now that the process memory has been saved to the file system, it can be pulled off the device and processed by a memory analysis tool such as [MAT](http://www.eclipse.org/mat/)

I've tried this with one of my devices, gathering heap dumps for a few different processes. Not too surprisingly, plenty of data I'd rather not have just anyone taking a peek at was readily available. In some cases, passwords were pointed out quite clearly.

For a legitimate software developer, this functionality can be great for debugging / troubleshooting purposes. However, for the everyday user, this is quite the opposite. A thief could swipe a given device and, if rooted, have access to a lot of live, possibly private, data. Unfortunately, password protecting your device does not prevent this. And, apps that secure data with passwords or encryption may be at risk too since the secured data could already be readable in memory.

Thankfully, Google has [closed this vulnerability](https://github.com/android/platform_dalvik/commit/b037a464512c0721bdca969ae19cce3d4b17b083#vm/SignalCatcher.c) as of [Android 2.3](https://github.com/android/platform_dalvik/commits/gingerbread-release/vm/SignalCatcher.c) by disabling heap dumps via the previously mentioned kill signal. This doesn't mean that devices running this software are impenetrable. But, it does make this type of hack a bit harder.

So, the moral of the story is that a malicious individual will likely find a way to get the information they want, if they're talented (some may prefer the term evil?) enough. However, if you value your privacy, you should be aware that you may be giving it away by rooting your Android devices.
