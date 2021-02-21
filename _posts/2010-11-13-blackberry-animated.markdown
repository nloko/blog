---
comments: true
date: 2010-11-13 05:15:20
layout: post
slug: blackberry-animated
title: 'Blackberry: Animated'
wordpress_id: 235
categories:
- Blackberry
- Java
- Programming
tags:
- Animation
- Blackberry
---

After using a few Blackberry applications, I noticed that many (if not all) of the them lack anything more than a very basic UI. So, I decided to take a peek and figure out why.

As it turns out, RIM hasn't provided an API for animations in their Blackberry SDK [until now](http://docs.blackberry.com/en/developers/deliverables/17966/Graphics_and_animation_overview_1240891_11.jsp). Now being OS 6.0. Yes, after six OS versions, they've finally realized that people enjoy a visually attractive and fun user experience. Better late than never, I guess.

So, what to do if you're writing apps for devices running anything less than OS 6.0? Googling the keywords "Blackberry animation" brings up very few hits. I did find a great[ example](http://stackoverflow.com/questions/1497073/blackberry-fields-layout-animation), however, on [stackoverflow.com](http://stackoverflow.com). I found that one particularly interesting, so I decided to work up a test based on it. It's very, very basic. But, the Animation class that materialized is something that could be very useful. See below:

~~~ java     
/**
 * Copyright 2010 Neil Loknath
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 ***/

package com.nloko.animationtest;

import net.rim.device.api.system.Display;

public class Animation {
	public static interface AnimationListener {
		void onNewFrame(int time);
	}

	private static final int DEFAULT_FPS = 40;

	private int _duration;
	private int _time;
	private int _fps = DEFAULT_FPS;
	private Thread _thread;
	private volatile boolean _running;

	private AnimationListener _listener;

	public Animation(int duration) {
		_duration = duration;
	}

	/**
	 * The number of frames in an animation per second
	 * @param fps
	 */
	public void setFPS(int fps) {
		_fps = fps;
	}

	public int getFPS() {
		return _fps;
	}

	/**
	 * The total duration of the animation
	 * @param duration
	 */
	public void setDuration(int duration) {
		_duration = duration;
	}

	public int getDuration() {
		return _duration;
	}

	/**
	 * The time elasped since the animation started
	 * @return
	 */
	public int getTimeElapsed() {
		return _time;
	}

	public void setListener(AnimationListener l) {
		_listener = l;
	}

	/**
	 * Start the animation
	 */
	public synchronized void start() {
		if (_thread == null) {
			_running = true;
			_thread = new Thread(new Runnable() {
				public void run() {

					final int idleTime = 1000 / _fps;
					final int duration = _duration;
					_time = 0;

					try {
						while(_running && _time <= duration) {
							animate(_time);
							_time += idleTime;

							Thread.sleep(idleTime);
						}

						if (_time - idleTime < duration) animate(duration);

					} catch (InterruptedException e) {}

					stop();
				}
			});

			_thread.start();
		}
	}

	/**
	 * Stop the animation
	 */
	public synchronized void stop() {

		_running = false;

		if (_thread != null && _thread.isAlive()) {
			_thread.interrupt();
			_thread = null;
		}
	}

	/**
	 *
	 * @param time
	 */
	private void animate(int time) {
		AnimationListener listener = _listener;
		if (listener != null) {
			listener.onNewFrame(time);
		}

	}
}
~~~ 

Without going into too much detail, what the class does is abstract away all the boring details of managing when and how often to display animated frames. All the user of the class needs to do is tell it the duration of the animation, when to start, and listen for events. To see it in action, here's a [sample project](/blog/images/animationtest.zip) that simply scrolls in the word "Hello" from the left and the word "World" from the top until they both meet in the centre to form the sentence (can you guess?) ..."Hello World!"

In the coming weeks, I hope to find the time to add an [Interpolator](http://en.wikipedia.org/wiki/Interpolation) to this class for rendering effects like acceleration, deceleration, and elastic effects ie. overshooting a target and bouncing back. Fun stuff!
