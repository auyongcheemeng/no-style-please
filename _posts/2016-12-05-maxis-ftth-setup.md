---
layout: post
title: "Maxis Fibre setup for custom routers (key essentials only)"
date: 2016-12-05 
categories: networking
tags: maxis ftth tomato
---

Researching on the interwebs on the topic of setting up a custom (non-maxis issued) router for use with Maxis fibre service yields no official infomation, only several guides/blogs/YT videos which are outdated, containing inaccurate info and burried in long forum discussion threads [guides by the likes of third parties, eg. networking hardware manufacturer(s), yes STILL outdated this time in writing 2021; (mis)infomation being echoed in that forum with */kopitiam/* ಠ_ಠ ] ; only lacking on all the key details required to properly configure a custom router. 

Since 2016, this post has been updated several times, *[link to the archived original post at the end of this page](#disclaimer)*. This post is written implicitly with the sole purpose for shedding light on key required information for custom router configurations. 

I will highlight the following point as many that come across this post fail to understand:

** THIS IS NOT a-step-by-step / how-to guide / tutorial **


#### Custom router requirements

> A capable router / managed switch with **IEEE 802.1Q / VLAN tagging**;    
> Both on **in-hardware** and **in-software** device support is required. 

Requirements: the above quote. 

Most consumer routers that is adverstised as 'unifi/maxis/time fiber compatible' is already doing VLAN tagging, as most/if not all of the Malaysian fiber ISPs are using vlans for their networks. 

The capabilities of these devices are limited by the firmware provided by the equipment manufacturer. Most of the home/consumer routers would be able to configure common defaults like `vlan 621` that provides the internet service. However these routers are often limited in flexibility to configure custom VLAN bridging for the full spectrum of other services that comes with the fiber internet service; ie. IPTV, VoIP etc. and that the configuration will vary across the ISPs.

As such, commercial/business class 'managed switches/routers' (eg. mikrotik, ubiquiti); or the use of opensource firmware (eg. openWRT, ddWRT, tomato,* etc) for capable consumer routers that provides the full flexibility in the configuring advanced networking features are HIGHLY recommended to properly configure vlan trunking/tagging/bridging.

### The key essentials:

    ##For Maxis Fibre on TM (HSBB) Infrastructure 
	VLAN VID `621` #for internet (PPPoE)
             `822` #for VoIP/SIP
             `821` #for TM management network (Maxis Fibre using TM infrastucture)
             `823` #for Broadband TV/IPTV service
    
	##For Maxis Fibre on Maxis Infrastructure
	VLAN VID `11` #for internet (PPPoE)
             `14` #for VoIP/SIP
             `6`  #for Maxis management network (Maxis's own fibre infrascructure)
             `17` #for Broadband TV/IPTV service
			 
**EDIT (March 2021):**     
Please see new section below [Privacy and Security Notes](#privacy--security-notes) for additional information on VLANs `821` and `6` for "Management network" as mentioned in the key essentials above
			 
Fast forward to 2018, the key essentials above is an *open secret* as it is all in plain view on the main web administration page of the stock Maxis issued Archer C5v. Back in 2016, I had to ask my network engineer contact at Maxis for all this information as it was not user accessable in the older hardware, and embeded in the routers' firmware / configuration. 

**Below:** Screenshot from my Maxis issued Archer C5v for Maxis Fibre on TM (HSBB) Infrastructure

![Maxis fibre TP-Link Archer C5v admin page configured for TM infra](/img/maxis-tp-link-c5v-archer.png)

**Below:** Screenshot courtesy of Afifi of his Archer C5v for Maxis Fibre on Maxis's own infrastruture

![Maxis fibre TP-Link Archer C5v admin page configured for MX infra](/img/maxis-tp-link-c5v-archer-mxinfra.png)

### Privacy & Security Notes
  
It should be noted that Maxis issued routers are configured by default for remote acesss using the [TR-069 protocol][TR-069] over VLANs `821` or `6` listed above. The protocol enables Maxis' technicians to remotely access the router for autoconfiguration [etc (see Wikipedia for further reading)][TR-069]. This feature *can be potentially abused* as the feature *can* behave like a backdoor, allowing silent full access to the router and network; ie. router reconfigured maliciously, connected devices traffic and wireless signals in proximity to the router monitored. 

If you do NOT want/intend to have Maxis' technicians to remotely reconfigure/have ability to remotely control your Maxis issued router OR are just privacy minded/values a-more-secure-no-backdoor network, VLANs `821` or `6` should NOT be enabled/forwarded to the Maxis issued router. (With that being said, with it disabled, Maxis cannot remotely mess with that router and at the same time: cannot remotely help you reconfigure it should you screw it up. You have been warned, use your own judgement and caution when considering this course of action)

Should you take the step of not using / disabling / blocking VLANs `821` or `6`; You might want to also dig through the Maxis issued routers' configuration using the root administrator (please dont ask me for the username and password; search for it) looking for the TR-069 option to also disable that for safe measure. You might also want to block network access to IP(s) and domain relating to the server at `acs069.maxis.com.my` (ACS as in *automatic configuration server* in TR-069 protocol terminology).

[TR-069]: https://en.wikipedia.org/wiki/TR-069

#### Disclaimer

The above information provided in good faith that the reader already has the *required minimum level of knowledge* on how to configure his/her own networking equipment, lacking only in the few essential details as mentioned above. 

I will NOT provide that knowledge. I also reserve the right to not answer / provide support requests to issues pertaining the usage of the key information provided (especially in cases relating to basic issues but not limited to this).

Should the reader of this post find him/herself having no clue what to do with the information above: This post is NOT intended for *you*.

-

### Post change log

    Sept 2021  - Post reorder; archiving original post

	March 2021 - Privacy/security notes on TR-069, VLAN 821,6

	Oct 2020   - Post rewised

    April 2020 - Post reorder; addition of disclaimer, requirements, etc.
    
    Jan 2019   - Key essentials updated w/ screenshot of Archer C5v configured 
                  for Maxis Fiber on Maxis's own fibre infrastructure.
    
    Oct 2018   - Maxis issued router TP-Link Archer C5v; vlan config details, 
                  key essentials updated.

    Jan 2018   - Post reorder.

    June 2017  - Voip section was edited for clarity/simplification.
    
    Dec 2016   - Original post.


-

For archived original post: [Maxis FTTH setup on custom router (tomato)][archived]

[archived]: /networking/2016/12/05/maxis-ftth-setup-archived.html

Misc: [Maxis Fiber with IPv6 setup on the Ubiquiti EdgeRouter-X](https://h.auyong.me/networking/2018/07/24/ipv6-on-maxis-fiber-with-erx.html)