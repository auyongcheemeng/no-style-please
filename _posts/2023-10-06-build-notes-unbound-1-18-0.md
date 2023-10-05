---
layout: post
title: build notes - unbound 1.18.0
date: 2023-10-06 03:02 +0800
category: build-notes
tags: server dns unbound
---
A quick build notes for my typical use case on compiling `unbound 1.18.0` for armhf on the Raspberry Pis

    # Getting build dependancies installed
    sudo apt-get install libssl-dev libexpat1-dev libnghttp2-dev libevent-dev libsystemd-dev libpython2-dev python-is-python2 swig libprotobuf-c-dev protobuf-c-compiler
 
    # Adapted configure options to include support for DoH
    ./configure --build=arm-linux-gnueabihf --prefix=/usr --includedir=${prefix}/include --mandir=${prefix}/share/man --infodir=${prefix}/share/info --sysconfdir=/etc --localstatedir=/var --disable-option-checking --disable-silent-rules --libdir=${prefix}/lib/arm-linux-gnueabihf --libexecdir=${prefix}/lib/arm-linux-gnueabihf --disable-maintainer-mode --disable-dependency-tracking --disable-rpath --with-pidfile=/run/unbound.pid --with-rootkey-file=/var/lib/unbound/root.key --with-libevent --with-pythonmodule --enable-subnet --enable-dnstap --enable-systemd --with-chroot-dir= --with-dnstap-socket-path=/run/dnstap.sock --libdir=/usr/lib --disable-flto --with-libnghttp2

Additional notes/articles/links include:
- [Unbound - DNS-over-HTTPS](https://unbound.docs.nlnetlabs.nl/en/latest/topics/privacy/dns-over-https.html)
- [Using unbound with Pi-hole - official documentation](https://docs.pi-hole.net/guides/dns/unbound/)

