---
layout: post
title: "Virtualbox extpack install (CLI)"
date: 2021-01-14
categories: bookmarks
tags: vmware software
---

*This one I always forget every now and then: I open up Virtualbox to update it and its extension pack, I have to do this. This time I'm bookmarking this in a post.*

For those of us for whatever reason can't just do the normal double click - install and needs to run the install in an system elavated command prompt. 

It's self explaintory below or refer to the reference documentation.

    VBoxManage extpack install --replace "updated_Extension_Pack.vbox-extpack"

Reference at time of writing of this post is :    
[Oracle® VM VirtualBox User Manual for Release 6.0 - Section 7.41: VBoxManage extpack][link]


[link]: https://docs.oracle.com/en/virtualization/virtualbox/6.0/user/vboxmanage-extpack.html