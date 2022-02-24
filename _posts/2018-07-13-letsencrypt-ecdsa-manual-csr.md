---
layout: post
title: "Let's Encrypt manual ECDSA certificate signing request"
date: 2018-07-13 
categories: bookmarks
tags: ssl
---

Just the bare essentials below (with my own modifications):

{% highlight bash %}
openssl ecparam -genkey -name secp384r1 | openssl ec -out ec.key
openssl req -new -sha256 -key ec.key -nodes -out ec.csr -outform pem
{% endhighlight %}

Depending on certbots ACME challenge methods preferred:
{% highlight bash %}
sudo certbot certonly \
	--dns-cloudflare --dns-cloudflare-credentials cloudflare_id.ini \
	-d h.auyong.me --csr ./ec.csr
{% endhighlight %}
{% highlight bash %}
sudo certbot certonly -w /var/www/ayhx/_site/ -d h.auyong.me --csr ./ec.csr
{% endhighlight %}

Source: [Using ECDSA certificates with Let's Encrypt](https://www.ericlight.com/using-ecdsa-certificates-with-lets-encrypt), 2016


