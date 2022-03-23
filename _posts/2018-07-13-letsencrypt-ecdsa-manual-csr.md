---
layout: post
title: "Let's Encrypt manual ECDSA certificate signing request"
date: 2018-07-13 
categories: bookmarks
tags: ssl
---

EDIT 2022: `certbot` v1.10 onwards does automate EC cert creation [with a config change](https://eff-certbot.readthedocs.io/en/stable/using.html#using-ecdsa-keys)

Just the bare essentials below (with my own modifications):

    openssl ecparam -genkey -name secp384r1 | openssl ec -out ec.key
    openssl req -new -sha256 -key ec.key -nodes -out ec.csr -outform pem

Depending on certbots ACME challenge methods preferred:

    certbot certonly \
        --dns-cloudflare --dns-cloudflare-credentials cloudflare_id.ini \
        -d h.auyong.me --csr ./ec.csr

    certbot certonly -w /var/www/ayhx/_site/ -d h.auyong.me --csr ./ec.csr

Source: [Using ECDSA certificates with Let's Encrypt](https://www.ericlight.com/using-ecdsa-certificates-with-lets-encrypt), 2016

