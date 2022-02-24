---
layout: post
title: "Public DNS servers (Google DNS, OpenDNS, Quad9, Cloudflare) on Maxis Fiber, Benchmarked "
date: 2018-04-06 
categories: networking
tags: dns
---

Benchmarked with GRC's [DNS Benchmark](https://www.grc.com/dns/benchmark.htm) tool on Maxis Fiber. Basically, your mileage will vary based on where these servers are relative to your location from your ISPs network. All of them are employing anycast IP addresses, where traffic to them will be routed to nearest server in your region. I prefer these servers rather than ISP provided ones due to their support of DNSSEC, (well except opendns, they have a similar, in function thing going on called DNSCRYPT) which prevent tampering of dns records.

Google's [Public DNS](https://developers.google.com/speed/public-dns/) is `8.8.8.8` and `8.8.4.4`    
Cisco's [OpenDNS](https://opendns.com) is `208.67.222.222`, `208.67.220.220` and `208.67.222.123`<sup>1</sup>     
[Quad9](https://www.quad9.net)'s is `9.9.9.9`, `149.112.112.112` and `9.9.9.10` <sup>2</sup>    
[Cloudflare](https://1.1.1.1)'s is `1.1.1.1` and `1.0.0.1`   

![DNS Benchmark, April 2018](/img/dnsbench-april-2018.png)

Selected graphical results above in text form below, ordered by fastest (cached) queries first:
All times measured is in seconds
```
    8.  8.  4.  4 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.004 | 0.005 | 0.007 | 0.001 | 100.0 |
  - Uncached Name | 0.012 | 0.077 | 0.304 | 0.090 | 100.0 |
  - DotCom Lookup | 0.175 | 0.217 | 0.304 | 0.041 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
             google-public-dns-b.google.com
                 GOOGLE - Google LLC, US


    1.  1.  1.  1 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.004 | 0.005 | 0.006 | 0.000 | 100.0 |
  - Uncached Name | 0.005 | 0.122 | 0.348 | 0.101 | 100.0 |
  - DotCom Lookup | 0.005 | 0.109 | 0.270 | 0.109 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
            1dot1dot1dot1.cloudflare-dns.com
        MEGAPATH2-US - MegaPath Networks Inc., US


    1.  0.  0.  1 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.004 | 0.005 | 0.007 | 0.001 | 100.0 |
  - Uncached Name | 0.007 | 0.129 | 0.336 | 0.098 | 100.0 |
  - DotCom Lookup | 0.005 | 0.116 | 0.269 | 0.108 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
            1dot1dot1dot1.cloudflare-dns.com
          CLOUDFLARENET - Cloudflare, Inc., US


    8.  8.  8.  8 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.004 | 0.006 | 0.008 | 0.001 | 100.0 |
  - Uncached Name | 0.014 | 0.073 | 0.377 | 0.093 | 100.0 |
  - DotCom Lookup | 0.171 | 0.214 | 0.305 | 0.046 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
             google-public-dns-a.google.com
                 GOOGLE - Google LLC, US
				 
				 
    9.  9.  9. 10 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.009 | 0.011 | 0.012 | 0.001 | 100.0 |
  - Uncached Name | 0.011 | 0.071 | 0.249 | 0.077 | 100.0 |
  - DotCom Lookup | 0.011 | 0.049 | 0.081 | 0.025 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
                   dns-nosec.quad9.net
                 QUAD9-AS-1 - Quad9, US


  208. 67.222.222 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.010 | 0.011 | 0.013 | 0.001 | 100.0 |
  - Uncached Name | 0.011 | 0.105 | 0.267 | 0.096 | 100.0 |
  - DotCom Lookup | 0.046 | 0.139 | 0.259 | 0.094 | 100.0 |
  ---<O-OOO-OO>---+-------+-------+-------+-------+-------+
                  resolver1.opendns.com
               OPENDNS - OpenDNS, LLC, US

			       
	9.  9.  9.  9 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.011 | 0.012 | 0.014 | 0.001 | 100.0 |
  - Uncached Name | 0.012 | 0.075 | 0.249 | 0.079 | 100.0 |
  - DotCom Lookup | 0.013 | 0.059 | 0.084 | 0.025 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
                      dns.quad9.net
                 QUAD9-AS-1 - Quad9, US


  208. 67.220.220 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.011 | 0.012 | 0.015 | 0.001 | 100.0 |
  - Uncached Name | 0.012 | 0.121 | 0.265 | 0.094 | 100.0 |
  - DotCom Lookup | 0.012 | 0.139 | 0.256 | 0.097 | 100.0 |
  ---<O-OOO-OO>---+-------+-------+-------+-------+-------+
                  resolver2.opendns.com
               OPENDNS - OpenDNS, LLC, US


  149.112.112.112 |  Min  |  Avg  |  Max  |Std.Dev|Reliab%|
  ----------------+-------+-------+-------+-------+-------+
  - Cached Name   | 0.012 | 0.014 | 0.015 | 0.001 | 100.0 |
  - Uncached Name | 0.013 | 0.080 | 0.267 | 0.084 | 100.0 |
  - DotCom Lookup | 0.015 | 0.057 | 0.086 | 0.023 | 100.0 |
  ---<-------->---+-------+-------+-------+-------+-------+
           rpz-public-resolver1.rrdns.pch.net
                 QUAD9-AS-1 - Quad9, US
```

Full benchmark [results [TXT]](/files/dns-benchmark-raw-2018.txt)
    
Notes:    
<sup>1</sup> [Cisco OpenDNS's Family Shield IP](https://www.opendns.com/home-internet-security/) filters some objectional content.    
<sup>2</sup> Quad9 filters some bad domains. `9.9.9.10` is their *no blocking* server to check against.    
<sup>3</sup> Fastest servers on 10.17.0.0/24 are my local servers running a combination of bind9 and dnsmasq