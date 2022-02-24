---
layout: post
title: "2021 Server Update - nginx 1.19.6 and OpenSSL 1.1.1i"
date: 2021-02-16 
categories: server
tags: nginx openssl
---

Havent done one of these in a while, not that I've havent been updating the server. Just that while working out build issues and figuring out which newer versions of nginx (1.17.3 and later) works with which versions of OpenSSL (1.1.x / 3.x.x), I've found the infomation lacking between posts in 2019 and 2021 reporting on working builds.

Here's my working build, compiled from (at time of writing latest) nginx source and OpenSSL 1.1.1i from github; for the Raspberry Pi 3:

{% highlight bash %}
 $ nginx -V
nginx version: nginx/1.19.6
built by gcc 8.3.0 (Raspbian 8.3.0-6+rpi1)
built with OpenSSL 1.1.1i  8 Dec 2020
TLS SNI support enabled
configure arguments: 
--with-cc-opt='-g -O2 -fPIE -fstack-protector-strong -Wformat -Werror=format-security -D_FORTIFY_SOURCE=2' \
--with-ld-opt='-fPIE -pie -Wl,-z,relro -Wl,-z,now' \
--sbin-path=/usr/sbin/nginx \
--prefix=/usr/share/nginx \
--conf-path=/etc/nginx/nginx.conf \
--http-log-path=/var/log/nginx/access.log \
--error-log-path=/var/log/nginx/error.log \
--lock-path=/var/lock/nginx.lock \
--pid-path=/run/nginx.pid \
--with-http_v2_module \
--with-http_ssl_module \
--with-http_realip_module \
--with-http_geoip_module \
--with-openssl=/usr/lib/openssl-dev-git \
--add-module=/usr/lib/headers-more-nginx-module-0.33
{% endhighlight %}
