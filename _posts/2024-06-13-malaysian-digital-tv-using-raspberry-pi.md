---
layout: post
title: Malaysian Digital TV using Raspberry Pi
date: 2024-06-13 11:40 +0800
tags: build-notes
---

Digital TV broadcast has been available in Malaysia since circa 2017. The common ways to get access to the broadcasts is to buy a new TV with a built-in digital tuner (DVB-T2) or get an external third-party decoder box. 

To some folks like me, neither option seems to be appealing as:

   1. Replacing an existing perfectly functional older TV without the digital tuner is wasteful and 
   2. *Privacy/security/long term support implications* of getting a new Internet connected Smart TVs or android based setup/decoder boxes.    
	These have gotten so cheap and you couldn't help to wonder if they are intentionally sold at a loss and [you are the product][] instead. Nor am I confident of the manufacturer's long term commitment to support the device with software fixes and security updates. 
	
Instead, I prefer hardware and software that doesn't have to rely entirely on the single manufacturer, eg. with the Pi and open source software.

---

This post serves as a quick configuration note for myself for configuring my Raspberry Pi servers for free over the air DVB-T2 reception in Malaysia. 

Required hardware/software package include:

   + Raspberry Pi (any of them will work**)
   + DVB-T2 tuner (linux compatible USB tuner/or my preferred [Pi TV HAT][])
   + `tvheadend` a linux PVR backend [[Github](https://github.com/tvheadend/tvheadend)]
   + a PVR client of your choice (eg. pvr client addonn with [kodi][] on [LibreELEC][]/[OSMC][] running on another Pi, or you can run on the same Pi as `tvheadend`)

** A faster Pi would be recommended as slower Pis, eg. 2 and below might suffer some slight audio/video sync issues. Issue can be solved by enabling MPEG2 codec hardware support. [MPEG2 decode/license key](https://codecs.raspberrypi.com/mpeg-2-license-key/) is required (I'm not sure if the licenses should still be required, as the patent on the codec should have expired worldwide by now)

![DVB-T2 mux settings for tvheadend](/img/malaysia-dvb-t2-tvheadend.png)

As of 2024, the broadcast seems to have stabilized using frequencies `650MHz`, `666MHz` in the greater Klang Valley/KL/Selangor area, frequency width is `8MHz`. For other areas  check [MYTV broadcast frequencies][MYTV]. For everything else, eg. constellation etc should set to `auto`.

In my experience, the digital broadcast signal may drop in and out when the signal is weak (depending on distance to transmitter, obstructions and weather conditions). You may need to reorient your directional antenna, eg. [rooftop Yagi antenna](https://en.wikipedia.org/wiki/Yagi%E2%80%93Uda_antenna) to point directly to your nearest broadcast transmission station (some research may be required, see [MYTV transmitter sites][MYTV])



[MYTV]: https://mytvbroadcasting.my/coverage/
[you are the product]: https://duckduckgo.com/?q=you+are+the+product
[Pi TV HAT]: https://www.raspberrypi.com/products/raspberry-pi-tv-hat/
[kodi]: https://kodi.tv/
[OSMC]: https://osmc.tv/
[LibreELEC]: https://libreelec.tv/