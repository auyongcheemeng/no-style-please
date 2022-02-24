---
layout: post
title: "Fujifilm NP-W126/S batteries and power related resources"
date: 2021-09-08 
categories: bookmarks
tags: fujifilm batteries
---
Dom Varney has written [a very detailed and informative article][article] on everything to know about powering a Fujifilm X-T3 and the battery it uses the NP-W126/NP-W126S which is applicable and relevent to every other X-series camera that uses the same battery type.

I came across his site in one of the photography forum threads while researching for a detailed schematic pin out for the CP-W126 to "fix" a non working third party DC coupler which only bothered to solder the leads to postive (+) and negative (-) pins on the blank unpopulated PCB in the dummy cell. 

To get it to work my X-Pro2 I needed to add a 10KOhm NTC (That is normally there in an actual NP-W126S battery) between the T terminal connection to ground (that is battery negative) on the proper spot on the PCB. An ordinary 10K ressistor would theoreatically work too, but i prefered the former as the NTC part was smaller and I didnt have any SMD 10K resistors at hand.

PCB pictured below after fix. Pardon my sub-optimal hand soldering jobby, PCB was meant to be heat gun soldered using SMD techniques. 

![PCB Third party CP-W128](/img/2021-09-08-thirdparty_cp-w126_1280px_web.jpg)


Link to Don's comprensensive write up: [https://domvarney.com/2018/11/22/powering-the-fuji-x-t3/][article]

Also, Dom wrote [about the larger capacity NP-W235 battery](https://domvarney.com/2020/04/29/fuji-np-w235-battery/) used on some newer Fujifilm cameras.


[article]: https://domvarney.com/2018/11/22/powering-the-fuji-x-t3/