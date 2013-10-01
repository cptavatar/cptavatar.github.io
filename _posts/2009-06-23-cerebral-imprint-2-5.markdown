---
author: admin
comments: true
date: 2009-06-23 21:10:24+00:00
layout: post
slug: cerebral-imprint-2-5
title: Cerebral Imprint 2.5
wordpress_id: 157
categories:
- Projects
tags:
- Cerebral Imprint
- Mac
---

Whew! I just finished a major rewrite on my flash card app, [Cerebral Imprint](http://www.alexrose.net/code/cerebral-imprint/). One of the early design decisions I made way, way back when I first wrote the application (ouch, was it really back in 2004?) was to make it a single document application. The application would store all its information about the user's data in a single file in the user's Library directory. This was simple, however as time went on and my personal flash card library grew I realized it just wasn't going to cut it.

The next thing I did was to hack on support for the application to read and write its flash card data to other files. When the application would start up it would prompt the user if they wanted to open an existing file or start a new one. Only one file could be open at a time but it was the least invasive way to get multiple file support without changing a lot of code (and how the user interface works). It worked but I wasn't really happy.

Thing is, there is way to this the right way. You base your application off [NSDocument](http://developer.apple.com/documentation/Cocoa/Conceptual/Documents/Tasks/ImplementingDocApp.html) and Cocoa provides all sorts of functionality for you. It was really bugging me that Cerebral Imprint wasn't acting like a normal document-based application for the Mac should behave so I decided on perhaps a overly drastic course of action - I started from scratch with a totally fresh NSDocument application and imported code as I needed from my old project. It took a lot of time but ultimately it was worth it since as I imported the old code I took the opportunity to scrub cruft going back in some cases to 2004 that was no longer being used and really clean things up.

I also added some new functionality along the way. For instance, I've been playing around with flash cards apps on my iPhone but haven't felt like tackling writing an iPhone app right now so I've added export functionality so I can export my cards into apps like [Notecards](http://digitalassertion.com/Notecards/) to tote with me.
