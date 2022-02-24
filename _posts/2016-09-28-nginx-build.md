---
layout: post
title:  "nginx build 1.11.4 with Debian/Raspbian native compile time options"
date:   2016-09-28
categories: server
tags: nginx
---
Adapted `--with-cc-opt` and `--with-ld-opt` options from builds on the official Raspbian repos.

{% highlight bash %}
nginx version: nginx/1.11.4
built by gcc 4.9.2 (Raspbian 4.9.2-10) 
built with OpenSSL 1.0.2i  22 Sep 2016
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
--with-ipv6 \
--with-http_realip_module \
--with-http_geoip_module
{% endhighlight %}

PS: newlines added to the original configure argument for text formating purposes