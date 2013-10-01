---
author: admin
comments: false
date: 2009-04-28 20:49:37+00:00
layout: post
slug: what-a-jaunty-macbook-you-have-there
title: What a Jaunty Macbook you have there...
wordpress_id: 139
categories:
- Tech
tags:
- Linux
- Mac
---

I've been taking another stab at dualbooting my Macbook1,1 with the release of [Ubuntu 9.04](http://www.ubuntu.com/products/whatisubuntu/904features/). As a mostly-happy Macophile, why dualboot you might ask? A couple of things - a weakness for playing around with Unix operating systems (a bad habit I picked up in college) and freakin Java 1.6. The problem is Apple decided not to release a 32bit version for 1.6 and my Macbook is the older Core Duo version and thus not supported. Now, normal people might sigh and stick to 1.5 or take this as an opportunity to buy a new laptop. The slightly more practical (or cheap) who refuse to give up probably turn to [soylatte](http://landonf.bikemonkey.org/static/soylatte/), the port of BSD to OS X (Metal L&F only - no pretty Mac L&F). I, however, with more disk space than sense, turned to [rEFIt](http://refit.sourceforge.net/) to set up a dual OS X/Linux setup.

I won't detail how to setup a dualboot system, there are enough tutorials out there if one searches for them. When I first setup my laptop I installed ubuntu  8.10 and quickly ran into  two annoyances  - an error message about my keyboard layout and the fact that by default the machine is very hard to use since the touchpad causes the cursor to jump around randomly while typing. Not in a mood to research them at the time, I got distracted and sadly it wasn't until 9.04 that I tried again. Both these problems persist with Jaunty so if you want to [run it on your it on your macbook](https://help.ubuntu.com/community/MacBook1-1/Jaunty), you are going to run into them.

The first issue manifests itself as an error message stating "Error activating XKB configuration" everytime you log into X. This is related to xorg not apparently knowing what to do with the macbook keyboard variant - there is an umbrella bug ubuntu uses to capture all these types of errors you can find [here](https://bugs.launchpad.net/ubuntu/+source/xkeyboard-config/+bug/67188). The solution is to modify your xorg.conf file to give X more information however I haven't dinked around with this yet since its just a minor annoyance.

The issue with the trackpad just about renders the machine unusable for anything but the most simplist tasks however its luckily easy to fix (or at least mitigate). In Jaunty, just add a startup application that looks like this:


> syndaemon -d


This will start up a program in the background every time you login that will disable the trackpad while you type, preventing it from causing the cursor to jump all over the screen. Syndaemon has a couple more options you can play with such as how long to disable the trackpad for but so far I'm finding the default settings to work ok.

A couple more random hints:



	
  * If you upgraded Jaunty and are now having problems with flash sites like Hulu telling you need flash 9 when you _know_ you had flash installed, try using synaptic to complete remove and then reinstall the flash-installer package - thats what it took for me  to get it working again on my living room media box.



	
  * If you are a [quicksilver](http://docs.blacktree.com/quicksilver/what_is_quicksilver) addict, check out [Gnome Do](http://do.davebsd.com/) - very slick and the keyboard shortcuts are even the same by default.


