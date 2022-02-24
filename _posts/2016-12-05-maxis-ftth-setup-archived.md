---
layout: post
title: "[Archived] Maxis Fibre setup for custom routers (key essentials only)"
date: 2016-12-05 
categories: networking
tags: maxis ftth tomato
---

#### Archived post below (no longer accurate); preserved for historical reference; Please refer to [an updated post][post] for proper updated (key essential) list of VLANs to be used and its application notes and security/privacy implications

[post]: /networking/2016/12/05/maxis-ftth-setup.html

(Dec 2016)

Long story short, I managed to get Maxis Fibre working with my custom router with VoIP after getting some unofficial help from a friend at Maxis. 
So, this is a shoutout to that person: Many thanks!

I used the Asus RT-AC66U router running the Tomato firmware (v1.28.0510.6 MIPSR2Toastman-RT-AC K26AC USB VPN) for the Maxis fibre (FTTH) service in a TM/Unifi (HSBB) area.

The details: Here's how it connects physically, the ethernet connection out of LAN2 (standard for UniFi/HSBB configured networks) from the optical network termination, (ONT), aka fibre modem, eg. Huawei EchoLife HG8240w; connects to the WAN port of the custom router. The custom router handles the Internet connection via PPPoE using Maxis provided username and password. 

(optional) Should you want to use the VoIP service provided, tagging traffic on a LAN port (of your choosing) and the WAN port on your router with vlan id **821**, **822**. This allows the VoIP traffic to pass between LAN port and the WAN port, and no where else. I used the Maxis issued Technicolor TG784nv3 router to handle the VoIP connection. The **Maxis router's WAN is plugged into the designated LAN** that you have chosen. No additional configuration is needed in the part of the Maxis issued router, the modem as configured by the service technician will work fine.

![Advanced VLAN setting in tomato's webUI](/img/vlan-tomato-for-maxis.png)

Notes: Screenshot above, in this older version of tomato, there is a [minor bug](http://tomatousb.org/forum/t-696297/wrong-port-order-in-gui-under-advanced-vlan-table): the ethernet ports on the VLAN page is numbered in reverse in firmware from the physical markings on the router. (eg. plugged physical ethernet cable into LAN4 port on the router, configure for the LAN1 port on the VLAN page as in image above). Newer subsequent version of Tomato based router firmware has this issue fixed.

PS: I've upgraded from the tomato router to an EdgeRouter X, perhaps I'll post an updated config for the ERX for maxis in a future post.

EDIT: [Maxis Fiber with IPv6 setup on the Ubiquiti EdgeRouter-X](https://h.auyong.me/networking/2018/07/24/ipv6-on-maxis-fiber-with-erx.html)