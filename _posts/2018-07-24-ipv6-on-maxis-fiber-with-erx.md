---
layout: post
title: "Configuring Edge Router X for IPv6 on Maxis"
date: 2018-07-24 
categories: networking
tags: erx
---

Leaving this config here in case someone else finds this useful. Configuration was done on the Ubiquiti EdgeRouter X, ERX (EdgeOSv1.10.5) for Maxis Fiber (HSBB Unifi infrastructure).

The typical Maxis Fiber internet connection is a PPPoE authenticated connection over VLAN 621. Hence in the config below IPv6 will be enabled under the PPPoE tree of the configuration directory.

In my config my actual LAN interfaces `eth2` and `eth3` is behind `switch0` interface. Hence I will be enabling ipv6 on the switch

Config as follows (in two parts):

    firewall {
        ipv6-name WANv6_IN {
            default-action drop
            description "WAN inbound traffic forwarded to LAN"
            enable-default-log
            rule 10 {
                action accept
                description "Allow established/related sessions"
                state {
                    established enable
                    related enable
                }
            }
            rule 20 {
                action drop
                description "Drop invalid state"
                state {
                    invalid enable
                }
            }
        }
        ipv6-name WANv6_LOCAL {
            default-action drop
            description "WAN inbound traffic to the router"
            enable-default-log
            rule 10 {
                action accept
                description "Allow established/related sessions"
                state {
                    established enable
                    related enable
                }
            }
            rule 20 {
                action drop
                description "Drop invalid state"
                state {
                    invalid enable
                }
            }
            rule 30 {
                action accept
                description "Allow IPv6 icmp"
                protocol ipv6-icmp
            }
            rule 40 {
                action accept
                description "allow dhcpv6"
                destination {
                    port 546
                }
                protocol udp
                source {
                    port 547
                }
            }
        }
    }

    interfaces {
        ethernet eth0 {
            duplex auto
            speed auto
            vif 621 {
                description "Internet (PPPoE)"
                pppoe 0 {
                    default-route auto
                    dhcpv6-pd {
                        pd 0 {
                            interface switch0 {
                                host-address ::1
                                prefix-id :0
                                service slaac
                            }
                            prefix-length 64
                        }
                        rapid-commit enable
                    }
                    firewall {
                        in {
                            ipv6-name WANv6_IN
                            name WAN_IN
                        }
                        local {
                            ipv6-name WANv6_LOCAL
                            name WAN_LOCAL
                        }
                    }
                    ipv6 {
                        address {
                            autoconf
                        }
                        enable {
                        }
                    }
                    mtu 1492
                    name-server auto
                    password ****************
                    user-id *******@public.maxis.com.my
                }
            }
        }
        switch switch0 {
            address 10.0.0.1/24
            ipv6 {
                address {
                    autoconf
                }
                dup-addr-detect-transmits 1
                router-advert {
                    link-mtu 1492
                    managed-flag true
                    name-server fe80::f369:71d6:f865:9974
                    name-server fe80::b1c3:b1cd:a709:ddc5
                    prefix ::/64 {
                        autonomous-flag true
                        on-link-flag true
                    }
                }
            }
        }
    }

Notes: 
1.   Maxis IPv6 uses a `::/64` prefix (as far as I can tell)
2.   `fe80::f369:71d6:f865:9974` and `fe80::b1c3:b1cd:a709:ddc5` are my local IPv6 DNS caching servers;    
Alternatively please feel free to use a public IPv6 DNS servers like [Google](https://developers.google.com/speed/public-dns/docs/using), [OpenDNS](https://www.opendns.com/about/innovations/ipv6/) or [Cloudflare](https://developers.cloudflare.com/1.1.1.1/setting-up-1.1.1.1/).
3. [Update 2021-10-06]    
   For the most part IPv6 does work on Maxis Fiber (ipv6.google.com etc), passes ipv6 test pages [[test ipv6][], [comcast ipv6 test][], [tlund.se IPv4/IPv6 test pages][] - passed all alternate pages except the IPv6 only and IPv6 only via cname pages, aparrently those dont exists/broken tests], and a non fullscore score on [internet.nl][].
4. [Update 2022-03-14]    
   Updated `router-advert: link-mtu 1492` to fix some adge cases mentioned in #3


[test ipv6]: https://ipv6-test.com/
[comcast ipv6 test]:http://test-ipv6.comcast.net/
[tlund.se IPv4/IPv6 test pages]: http://ipv4.tlund.se/
[internet.nl]: http://http://conn.internet.nl/connection/

### Disclaimer
(update March 2021)

The above post is NOT a how-to / step-by-step / tutorial

If the above does not make sense to you OR you do not know what to do with the information provided: This post is simply NOT for you. I will not provide the basic knowledge required to understand and properly configure your Edge Router. To thoso who's inclined to do it themselves, please read up at [Ubiquiti's Edgerouter Documentation Page](https://help.ui.com/hc/en-us/sections/360008075214-EdgeRouter). 

Please *DO NOT* contact me for support/assistance (especially issues related to basic knowledge of router configuration but not limited to this). Your network equipment is your own responsibility to configure and maintain.

TL;DR Information above is provided as it is; no more no less; for the benefit to those who can understand it; no support from the author will be provided; you are on your own.

### Post changelog

    2019-10-22 - After changes to Maxis's network and a year later of ERX firware patches the config below seems to be broken. Haven't gotten around to get it working again.
    
    2020-06-12 - The config above is still working. (Thanks to Andrew!).

    2021-03-07 - Added disclaimer section.
    
    2021-10-06 - Added notes to some edge case issues
    
    2022-03-14 - Added mtu options to fix some edge cases (ssl handshakes failing on certain servers)