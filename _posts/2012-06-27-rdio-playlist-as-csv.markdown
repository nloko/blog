---
comments: true
date: 2012-06-27 22:59:53
layout: post
slug: rdio-playlist-as-csv
title: Rdio Playlist as CSV
wordpress_id: 520
categories:
- Javascript
- Programming
---


So, you use [Rdio](http://rdio.com). You've created some kick-ass playlists. But, now you need to export them. Maybe you like having backups? Or, maybe you need to give a song list to a DJ? (like I needed to) Whatever the reason, you need to export them. But, Rdio has no export feature. What to do?

Enter this [bookmarklet](http://en.wikipedia.org/wiki/Bookmarklet) I whipped up. Slap the below code in a bookmark, save it, click while viewing an Rdio playlist, and you'll have yourself a new tab containing a comma delimited file in _Track Name, Artist, Album_ order.

{% gist 3001053 %}

This will work until Rdio changes their HTML. But, hopefully, they'll [provide the functionality themselves](http://help.rdio.com/customer/portal/questions/22160-export-playlists-to-excel) first.
