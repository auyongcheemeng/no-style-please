---
layout: post
title: 2022 Server Update - RaspPi 4 w/ Bullseye
date: 2022-02-25 03:59 +0000
category: server
---
It's one of those - havent done in a while updates. Earlier last year, the [Raspberry Foundation released a newer version of their Raspberry PI OS based on Debian 11 (Bullseye)](https://www.raspberrypi.com/news/raspberry-pi-os-debian-bullseye/), which brings many improvements (and also potential issues when upgrading over an existing installs). I've bit the bullet and did the in place upgrade on some of my Pi machines, with mixed results of sucesss. One critical piece (then) that wasn't able to sucessfully complete the upgrade was this server.

Sometime early this year, I've decided to upgade the older server to newer hardware. I dusted off the dust from the new Pi 4 model B that I have had for a long while (in storage), and installed the brand new fresh image for a new server. Despite having more than one of these I can't afford the plug space for all of them, multi-port (more than 2 port) USB-C wall power supplies do not yet exists, affordable ones at least. One nice thing about the upgrade is that, the upstream package repository for code is much more to date to compared to the ones in Buster. I don't have to manually fetch the latest source code and compile them for the newer features in versions of `nginx` and `unbound`.

Horray for a few more less things to do manually.