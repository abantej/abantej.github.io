---
layout: post
title:  "How to connect to WPA2 Enterprise in Raspbian OS (Raspberry Pi)"
date:   2019-11-15 05:39:00  +0800
categories: raspberry
---

This guide will teach you how to connect to a WPA2 Enterprise secured network.


### /etc/network/interfaces

{% highlight sh %}

source-directory /etc/network/interfaces.d

auto lo
iface lo inet loopback

iface eth0 inet manual

allow-hotplug wlan0
iface wlan0 inet manual
pre-up wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
post-down killall -q /etc/wpa_supplicant/wpa_supplicant.conf

{% endhighlight %}


### /etc/wpa_supplicant/wpa_supplicant.conf

{% highlight sh %}
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="NetworkName"
    scan_ssid=1
    key_mgmt=WPA-EAP
    group=CCMP TKIP
    eap=PEAP
    identity="username"
    password=hash:a6fsfs71xxxxxxxxxxxxxxxetcetcetc
    phase1="peapver=0"
    phase2="MSCHAPV2"
    disabled=0
}

network={
    ssid="NetworkName2"
    key_mgmt=NONE
    disabled=1
}
{% endhighlight %}

### Hash password for security

{% highlight sh %}

echo -n 'PASSWORD' | iconv -t utf16le | openssl md4 > hash.txt

{% endhighlight %}

### Clear .bash_history

{% highlight sh %}

~/.bash_history

{% endhighlight %}

### To open browser with proxy server settings

{% highlight sh %}

chromium-browser --proxy-server="https://128.0.0.1:8080" <web_url>

{% endhighlight %}