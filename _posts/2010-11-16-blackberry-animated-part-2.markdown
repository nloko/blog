---
comments: true
date: 2010-11-16 03:58:02
layout: post
slug: blackberry-animated-part-2
title: 'Blackberry: Animated Part 2'
wordpress_id: 256
categories:
- Blackberry
- Java
- Programming
tags:
- Animation
- Blackberry
---

In my last [post](http://nloko.ca/?p=235), I wrote about the lack of animation API provided in the Blackberry SDK. Sure, OS 6.0 provides some means for doing [animations](http://www.blackberry.com/developers/docs/6.0.0api/net/rim/device/api/animation/Animation.html), and OS 5.0 added an API for [screen transition](http://www.blackberry.com/developers/docs/5.0.0api/net/rim/device/api/ui/TransitionContext.html) animation. But, that's not enough for developers targeting devices running earlier OS versions. According to some [numbers](http://www.berryreview.com/2010/10/07/sensobi-releases-data-on-users-blackberry-os-versions) I dug up, there are still quite a few users running OS 4.6. So, the fact that OS fragmentation exists can't be ignored. Maybe, at some point in the future when all Blackberry users are running OS 6.0 and up, animated UIs will be a lot easier to create and maintain. But, until then, a lot of the work is left up to the developer.

The simple [example](/blog/images/animationtest.zip) of field layout animation I provided previously works great, but it's missing something. When watching those fields slide into place, I'm reminded of an Atari 2600 video game. The animation is too stiff and robotic. It needs life. It needs the help of [easing curves](http://docs.blackberry.com/en/developers/deliverables/17967/Easing_curves_1224328_11.jsp). An ActionScript developer by the name of [Robert Penner ](http://www.robertpenner.com/)posted a [chapter](http://www.robertpenner.com/easing/penner_chapter7_tweening.pdf) from a book he's written that gives an excellent introduction to the concept of easing curves. In addition, he's [published](http://www.robertpenner.com/easing/) a bunch of easing equations and [licensed them](http://www.robertpenner.com/easing_terms_of_use.html) under the [BSD license](http://www.opensource.org/licenses/bsd-license.php). If you have any interest at all in this kind of stuff, I highly recommend taking a look at his work.

With the help of Penner's work, I've [added](/blog/images/interpolatedtest3.zip) an overshoot interpolator to the original animation example I wrote. This makes the two text fields overshoot their targets and decelerate into position. It makes for a much more lively and fluid visual. In addition to this, I've created two other example projects. The [first](/blog/images/interpolatedtest2.zip) one demonstrates what could be called an elastic or bounce effect. The field being animated, captioned "Boing," bounces into its target position like it's attached to a bungee cord. It can be a great effect when used to drop things like status messages, for example, into place for a brief period of time and then pulling them out of view. This example shows how the dynamic positioning of the animated field can have an interesting cascading effect on the fields around it. The [last](/blog/images/interpolatedtest1.zip) example, however, eliminates that cascading effect and simply overlays the animated field over top the others.

As far as performance is concerned, these examples are probably not going to set any FPS records. They rely on the [updateLayout](http://www.blackberry.com/developers/docs/3.6api/net/rim/device/api/ui/Field.html#updateLayout()) method provided by the framework's [Field](http://www.blackberry.com/developers/docs/3.6api/net/rim/device/api/ui/Field.html) class. When called, it triggers the [sublayout](http://www.blackberry.com/developers/docs/3.6api/net/rim/device/api/ui/Manager.html#sublayout(int,%20int)) method of the containing [Manager](http://www.blackberry.com/developers/docs/3.6api/net/rim/device/api/ui/Manager.html) (which is a subclass of Field). A more efficient method may be to bypass the layout and directly paint objects on the screen. Instead of calling updateLayout on each notification from the Animation class, a call to the Manager's [invalidate](http://www.blackberry.com/developers/docs/3.6api/net/rim/device/api/ui/Manager.html#invalidate()) method could be performed instead. That would, in turn, trigger its contents to be painted. The contents could be fields, shapes, text, bitmaps, or whatever. But, unless your application is really busy, I'm assuming that the updateLayout method will be acceptable. I have yet to actually try these techniques in an application, so I could be wrong.

I'll leave you with a short screencast of one of the example projects in action. It's really not a great visual of the animation, as it looks choppier than it actually runs on the simulator. But, perhaps it will be enough to get you excited about adding animations to your applications too!



[Hello World](http://vimeo.com/16873867) from [Neil Loknath](http://vimeo.com/user5236378) on [Vimeo](http://vimeo.com).
