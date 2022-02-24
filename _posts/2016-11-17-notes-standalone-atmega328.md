---
layout: post
title: "Notes on standalone ATmega328 build"
date: 2016-11-17 
categories: maker
tags: arduino
---
Based on *Building an Arduino on a Breadboard*, a community tutorial on [Arduino][1]'s official site.

The minimalist materials list:

- 7805 Voltage regulator
- 2x 220 Ohm resistors
- 1x 10k Ohm resistor
- 2x 10 uF capacitors
- 16 MHz clock crystal
- 2x 22 pF capacitors

Removed items (common in stock items): 
- Breadboard
- 22 AWG wire
- 2x LEDs
- (optional) small momentary normally open ("off") button, i.e. Omron type B3F

USB to Serial Communication Board:

- FT232RL USB to Serial Breakout Board, SKU BOB-0071 OR
- Arduino Serial USB Board, SKU DEV-08165 


[1]: https://www.arduino.cc/en/Main/Standalone