---
layout: post
title: "These Thumbs Aren't Made For Scrolling"
date: 2015-01-11 17:01:24 -0500
comments: true
categories: UI UX Web 
---

Collapsible interfaces are great. [Bootstrap's Collapse](http://getbootstrap.com/javascript/#collapse) element comes to mind. As does [Wikipedia's collapsible sections](http://en.m.wikipedia.org/wiki/Mobile_phone) you get when viewing from a Mobile. They make it simple to compact a lot of information into a small space. They allow you to easily jump around a document giving you the choice of expanding one section at a time so less scrolling is required. But, what happens when you want to make things compact again? What if you've expanded something, scrolled through it, and now want to move on to another section? You have to either scroll all the way back to the top or bottom of the section, depending on which direction you want to go. This can really make for some tired thumbs on a mobile device.

Sure, we could implement one of those [trendy scroll-to-top](http://davidwalsh.name/demo/top-of-page-jquery.php) arrows. That at least let's you work your way up. But, what about the other direction? I think we can do better.

Below, on the left, you'll find the usual collapsing section user experience you know and love. On the right, you'll find the same interface with a subtle improvement.


<table  border="0" style="margin:auto;">
<tr>
<th>Without Improvement</th>
<th>With Improvement</th>
</tr>
<tr>
<td>
<iframe style="border: 1px solid #ddd;border-radius: 4px;margin: 10px;"  height="480" width="320" src="/collapse_demo_before.html" seamless>
<p>Your browser sucks.</p>
</iframe>
</td>
<td>
<iframe style="border: 1px solid #ddd;border-radius: 4px;margin: 10px;"  height="480" width="320" src="/collapse_demo_after.html" seamless>
<p>Your browser sucks.</p>
</iframe>
</td>
</tr>
</table>

You'll notice that the one of the right let's you collapse the section you're browsing even after you've zoomed past its title. This lets you move up and down without the thumb workout. The title also shinks a bit to give you that little bit of extra real estate. Pretty nifty, eh?
