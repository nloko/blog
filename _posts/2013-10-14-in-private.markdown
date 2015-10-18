---
layout: post
title: "In Private"
date: 2013-10-14 21:45
comments: true
categories: internet, security 
---

This [blog](https://www.nloko.ca/blog) and the entire [site](https://www.nloko.ca) are now 
only accessible using [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure).

Why
---
The reasons why I did this are fairly simple:

- I read [this](https://www.tbray.org/ongoing/When/201x/2012/12/02/HTTPS).
- And, I completely, 100% agree.

How
---
I got my SSL certificate from [StartSSL](http://www.startssl.com/) for free. They verified that
my site is really run by me in a matter of minutes. I moved my site from [NearlyFreeSpeech](https://www.nearlyfreespeech.net/) (nothing against them, as they were nothing but fantastic during the many years my blog was hosted there) to my VPS.
This gave me full control over things and allowed me to configure Apache to use SSL.

If you try to go to http://www.nloko.ca or http://nloko.ca or http://www.nloko.ca/anywhere you will be redirected to the same URL with
the scheme changed from HTTP to HTTPS.

Privacy by Default
------------------
This has nothing to do with secrecy. It's about your right to browse content on the Internet in private without anyone else listening in.
If you host a website, I urge you to consider making it private by default.
