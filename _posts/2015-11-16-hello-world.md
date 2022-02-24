---
layout: post
title:  "Hello World! and Server Updates"
date:   2015-11-16 22:29:05 +0800
categories: server update
---
This is my version of the example file written in Markdown for *Jekyll* in the `_posts` directory. 

You can consider this post as the *lorem ipsum* of sorts.

## Server Update

![RPi updating to Jessie](/img/rpi-jessie-update.png)

I had the pleasure of manually updating the Raspbian on the Pi from wheezy to jessie thanks to the folks at [stackexchange][].

In summary it was just the following commands to get The Pi up to date on wheezy before the distro update

{% highlight bash %}
apt-get update
apt-get upgrade
apt-get dist-upgrade
{% endhighlight %}

Followed by modifying the strings `wheezy` to `jessie` in repository config files listed below

{% highlight bash %}
/etc/apt/sources.list
/etc/apt/sources.list.d/*
{% endhighlight %}

And finally these `apt-get` again to get things to updated to newer versions

{% highlight bash %}
apt-get update
apt-get upgrade
apt-get dist-upgrade
{% endhighlight %} 

[stackexchange]: http://raspberrypi.stackexchange.com/questions/27858/upgrade-to-raspbian-jessie