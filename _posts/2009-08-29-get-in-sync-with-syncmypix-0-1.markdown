---
comments: true
date: 2009-08-29 09:18:00
layout: post
slug: get-in-sync-with-syncmypix-0-1
title: Get in Sync with SyncMyPix 0.1
wordpress_id: 20
categories:
- Android
tags:
- Android
- SyncMyPix
---

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/SpjgYls1fbI/AAAAAAAABNw/whJazm-knsM/s400/syncpix.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/SpjgYls1fbI/AAAAAAAABNw/whJazm-knsM/s1600-h/syncpix.png)

Staying in true geek form, since [GSoC](http://code.google.com/soc/) ended, I decided to take a "break" and tinker around with some [Android development](http://developer.android.com/intl/fr/index.html). What you see above, is a screenshot from the fruits of my labour over the past week or so. I call it SyncMyPix.

Originally, my inspiration came from Blackberry. My girlfriend's Pearl has a feature that allows her to automatically sync up her contacts' pictures with [Facebook](http://www.facebook.com/). So, I thought, "Hey, I want my phone to do that." And, with SyncMyPix, now it can. I figured it'd be a cool little app to try out as my first Android application.

Here's a run down of the features currently implemented:

* Sync your phone's contacts with your Facebook friends' profile pictures
* If do not want to overwrite manually set contact pictures on your phone, the Skip if non-SyncMyPix picture exists option will let you do that
* If a Facebook friend matches up with multiple contacts, you can skip them by checking the Skip if multiple phone contacts found option
* Sync runs in the background leaving you free to do other tasks
* View the results of the last sync operation

[![](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjgYC-s_eI/AAAAAAAABNo/4c59HlRuqIA/s400/syncpix+-+select.png)](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjgYC-s_eI/AAAAAAAABNo/4c59HlRuqIA/s1600-h/syncpix+-+select.png)

I decided that with so many social networks around these days, the app shouldn't be made specifically for Facebook (even though all it can handle is Facebook, right now). In the future, I'd like to add more sync sources. Maybe using the [OpenSocial API](http://code.google.com/apis/opensocial/).

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjgnat-qKI/AAAAAAAABN4/klcffs16dfs/s400/syncpix+-+menu.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjgnat-qKI/AAAAAAAABN4/klcffs16dfs/s1600-h/syncpix+-+menu.png)[![](file:///home/neil/Desktop/syncpix%2520-%2520select%2520source.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spb1BVVMWGI/AAAAAAAABMI/UMbVOUrhTSo/s1600-h/syncpix.png)

I used Android's built in menu system for the actions you see above. It's a much cleaner interface than a bunch of buttons.

[![](http://1.bp.blogspot.com/_d0oLVL7lqBw/Spb1d6NtqqI/AAAAAAAABMg/Bmg-zVVkbIc/s400/syncpix+-+login.png)](http://1.bp.blogspot.com/_d0oLVL7lqBw/Spb1d6NtqqI/AAAAAAAABMg/Bmg-zVVkbIc/s1600-h/syncpix+-+login.png)

The login action loads up the Facebook login webpage within a [WebKit embedded widget](http://developer.android.com/intl/fr/reference/android/webkit/WebView.html).  I've actually written a [tiny, weeny Facebook Java library](http://code.google.com/p/simply-facebook/) which I make use of here to interact with the [Facebook REST API](http://wiki.developers.facebook.com/index.php/API). After logging in, you'll also have to authorize the application, so it can access the API. As you can see, I'm letting Facebook do all the authentication work by directing you to their site.

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjg04xUYyI/AAAAAAAABOA/oClsBv4ij_w/s400/syncpix+-+thanks.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjg04xUYyI/AAAAAAAABOA/oClsBv4ij_w/s1600-h/syncpix+-+thanks.png)

After logging in, you get brought back to the original screen.

[![](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjhF_3dJXI/AAAAAAAABOI/_MnX_a3yHBo/s400/syncpix+-+starting.png)](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjhF_3dJXI/AAAAAAAABOI/_MnX_a3yHBo/s1600-h/syncpix+-+starting.png)

Now that the user has been authenticated, a sync operation can begin. After clicking the "Sync" menu option, a [notification](http://developer.android.com/intl/fr/guide/topics/ui/notifiers/notifications.html) is sent...

[![](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjhOcVny1I/AAAAAAAABOQ/WOjeBqQQpZA/s400/syncpix+-+notify.png)](http://3.bp.blogspot.com/_d0oLVL7lqBw/SpjhOcVny1I/AAAAAAAABOQ/WOjeBqQQpZA/s1600-h/syncpix+-+notify.png)

...and the sync gets underway. During the sync operation, SyncMyPix will attempt to match up your social networking friends' names with your phone's contact names. Name matching is currently very strict. As an example, a social networking friend named "Billy Bob" will match the following contacts on your phone:

* Billy Bob
* Bob, Billy
* Bob,Billy

[![](http://1.bp.blogspot.com/_d0oLVL7lqBw/SpjhiQ3Zi0I/AAAAAAAABOY/mjlKN01NPBE/s400/syncpix+-+progress.png)](http://1.bp.blogspot.com/_d0oLVL7lqBw/SpjhiQ3Zi0I/AAAAAAAABOY/mjlKN01NPBE/s1600-h/syncpix+-+progress.png)

The sync operation takes place in a [separate thread](http://android-developers.blogspot.com/2009/05/painless-threading.html), so the UI is free for the user to do whatever they want. If the HOME key is pressed, the user can come back to SyncMyPix by re-launching the application or clicking on the SyncMyPix notification. If the sync is still in progress, the progress bar will be displayed.

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjh9-hA-II/AAAAAAAABOg/QlGkhIrCQHo/s400/syncpix+-+done.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spjh9-hA-II/AAAAAAAABOg/QlGkhIrCQHo/s1600-h/syncpix+-+done.png)

Once the sync is complete, you'll get a [friendly message](http://developer.android.com/intl/fr/reference/android/widget/Toast.html) telling you so.

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spb1xk8vJxI/AAAAAAAABNQ/Jogdft9kRHs/s400/syncpix+-+results.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/Spb1xk8vJxI/AAAAAAAABNQ/Jogdft9kRHs/s1600-h/syncpix+-+results.png)

Then, you can click the "Results" menu option and see exactly what happened (names have been blurred to respect my friends' privacy).

As you can see, the application is a no-frills, just get it done type of app. The code and UI could use some polish, but it's in a decent, very usable state as is.

[![](http://2.bp.blogspot.com/_d0oLVL7lqBw/SpjicCCP4AI/AAAAAAAABOo/DWe_I_7jd3c/s400/icon.png)](http://2.bp.blogspot.com/_d0oLVL7lqBw/SpjicCCP4AI/AAAAAAAABOo/DWe_I_7jd3c/s1600-h/icon.png)

With a brand, spankin' new 48x48 icon, hot off the [Inkscape](http://www.inkscape.org/) press, I've just launch SyncMyPix 0.1 on the Android market. It's available for free, and I hope some will get some use out of it. So next time you're in the market for a new app, give mine a try. You can search for it in the Android market, or, if you're browsing this page from your Android phone, here[ is a direct link](http://market.android.com/search?q=SyncMyPix).


Look for the following new features in the future:
	
* An improved "Results" interface where the picture downloaded from a social network is displayed when selecting a friend from the list
* Manual conflict resolution in the "Results" interface where a long press on a friend would allow the picture to be manually added to a contact of the user's choosing
* A new "Progress" interface where the progress bar is integrated in the screen and an image widget displays the last picture downloaded
* Automatic scheduling of the picture download service with configurable frequency
* Improved extensibility with more social networking sites as picture sources
* Improved name matching
