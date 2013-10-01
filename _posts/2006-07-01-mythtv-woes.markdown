---
author: admin
comments: true
date: 2006-07-01 06:06:16+00:00
layout: post
slug: mythtv-woes
title: MythTV woes
wordpress_id: 27
categories:
- Tech
tags:
- Linux
---

I used to run [Knoppmyth](http://www.mysettopbox.tv/knoppmyth.html) on my home theater PC since it made the setting up and installation of [MythTV](http://www.mythtv.org/) a breeze, especially on my old [VIA EPIA](http://www.epiacenter.com/modules.php?name=Content&pa=showpage&pid=21) box. I recently retired that box and decided get everything set up on a AMD64 based shuttle pc.
I wanted to go back to using a full blown distro since I use the box for a lot more than MythTV. I had good experience with [Ubuntu](http://www.ubuntu.com/) in the past so grabbed the latest Dapper install iso and proceeded to get everything set up. I quickly ran into a complication - I wanted to reuse the mysql database from my previous installation so that my new box knew about what shows I had seen already and what I had recorded but had yet to watch. The version of KnoppMyth I was using was based on MythTV 19.0 but the only version in the Ubuntu repositories was 18.1 and the database schemas are not compatible. < sigh >
Looking over the Ubuntu forums I was able to find someone who had packaged up 19 and proceed to get everything installed just fine. Or at least it appeared, turns out the version I'm using has a problem where MythTV occasionally forgets about upcoming recordings. Restarting the backend solves the problem but I don't want to force restart the backend every 30 minutes since it would create annoying gaps if I restarted the backend while I was recording something. I thought about jumping through all the hoops required to rebuild MythTV from scratch myself but I didn't feel like going through the trouble right now so I came up with a short term hack.
I grabbed the latest version of mythweb and copied it into my apache2 root directory. Getting it working was as simple as creating a symlink to enable mod_rewrite and uncommenting a line in my PHP config to enable the mysql library. Once that was in place I wrote a simple script to wget the upcoming recordings, test to see if there was anything upcoming, and kick the backend if there wasn't. I then hooked it into a cron job to run at 5 minutes before every half hour. Its a band aid that should hold me until they get 19 into the tree.
#!/bin/bash
wget -q -O- http://192.168.1.5/mythweb/tv/upcoming | grep -q list_separator
if [ $? -ne 0 ]; then
/etc/init.d/mythtv-backend restart
fi
