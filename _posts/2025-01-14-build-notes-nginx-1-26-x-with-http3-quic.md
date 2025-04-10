---
layout: post
title: build notes - nginx/1.26.x with HTTP3/QUIC support
date: 2025-01-14 02:29 +0800
category: server
tags: nginx http3 quic
---

    nginx version: nginx/1.26.2
    built by gcc 12.2.0 (Raspbian 12.2.0-14+rpi1)
    built with LibreSSL 4.0.0
    TLS SNI support enabled
    configure arguments: --with-cc-opt='-g -O2 -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2 -I../libressl/build/include' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -fPIC -L../libressl/build/lib' --prefix=/usr --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-compat --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_v3_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_sub_module --add-module=/git/ngx_http_geoip2_module-3.4/ --add-module=/git/headers-more-nginx-module-0.34/ --with-openssl=../libressl

General build arguments was adapted from default distro (Rasbian/Raspberry Pi OS) builds and some customizations for my specific uses. 

LibreSSL source location was specified relative (and was symlinked, ie `ln -s /path/to/libressl-version-no/ libressl`) to the working directory.

References:
+ [NGINX.org - Support for QUIC and HTTP/3](https://nginx.org/en/docs/quic.html)

