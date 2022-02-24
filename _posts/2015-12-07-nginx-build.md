---
layout: post
title:  "nginx build 1.9.7 with experimental http2"
date:   2015-12-07 08:00:00 +0800
categories: server
tags: nginx
---
On the note of exciting news about [http2 adoption](http://techcrunch.com/2015/12/03/cloudflare-turns-on-http2-for-all-of-its-users/), I'd recompiled nginx in the Pi Server with HTTP2 support.


{% highlight bash %}
nginx version: nginx/1.9.7
built by gcc 4.9.2 (Raspbian 4.9.2-10) 
built with OpenSSL 1.0.1k 8 Jan 2015
TLS SNI support enabled
configure arguments: 
configure arguments: --with-http_v2_module \
--with-http_ssl_module \
--with-ipv6 --without-http_proxy_module \
--sbin-path=/usr/sbin/nginx \
--conf-path=/etc/nginx/nginx.conf \
--pid-path=/var/run/nginx.pid \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log 
{% endhighlight %}
