---
layout: post
title: build notes - tor 0.4.8.9/0.4.8.10
date: 2023-12-09 11:04 +0800
category: server
tags: tor build-notes
---
Quick notes on `tor 0.4.8.9/0.4.8.10` from source for my use case building on  Raspberry Pi 32 bit `armhf`.

    # Tor Official Repository (for source)
    deb-src [arch=armhf signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org bookworm main

    # Some additional dependencies needed as of Raspberry Pi OS / Debian 12 (Bookworm)
    sudo apt-get install libev-dev libssl-dev zlib1g-dev liblzma-dev libzstd-dev 

    # Build config option for drop in replacement for repo installed version
    ./configure --build=arm-linux-gnueabihf --sysconfdir=/etc --mandir=/usr/share/man --sbindir=/usr/sbin --bindir=/usr/bin

Additional notes/resources:    
[Tor Project - Installing from source](https://community.torproject.org/onion-services/setup/install/#installing-tor-from-source)    
[Tor Project - Debian Repository](https://support.torproject.org/apt/tor-deb-repo/) for `apt source` the newest version.
