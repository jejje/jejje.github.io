---
title: Sync Two PiHole DNS Servers for Failover
date: '2021-01-30 14:42:15'
author: JejjE
layout: post
permalink: "/2021-01-30-sync-two-pihole-dns-servers-for-failover"
categories:
- Networking
- DNS
tags:
- code
- shell
- DNS
banner_image: "/networking-patch-panel.jpg"
---

I use the very popular PiHole as my home DNS server to remove all ads from my network. It's great but having only one DNS server is setting up yourself for failure. In this post I'm going to show you how to sync the dns using RSYNC.
<!--more-->

![PiHole Dashboard](/images/posts/pihole.png)
## Raspberry Pi Zero W

PiHole is very efficient and can be run by almost any Raspberry Pi model you might have. [ Raspberry Pi Zero W ](https://www.raspberrypi.org/products/raspberry-pi-zero-w/) is really cheap, low powered and quiet. It doesn't have Ethernet but this model of the Pi has Wifi. 

<a title="Gareth Halfacree from Bradford, UK, CC BY-SA 2.0 &lt;https://creativecommons.org/licenses/by-sa/2.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Raspberry_Pi_Zero_W_(33209067455).png"><img width="512" alt="Raspberry Pi Zero W (33209067455)" src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Raspberry_Pi_Zero_W_%2833209067455%29.png/512px-Raspberry_Pi_Zero_W_%2833209067455%29.png"></a>

I bought the Pi Zero W which has only 512mb RAM and a single core, but that is enough for a small home network. With only one PiHole DNS server I had Internet trouble everytime I rebooted the server. As you might know, if DNS fails the whole Internet fails. That's why it's good that I bought two!
## Two DNS is the minimum
One of the best things with a home DNS server is that you can give your local IP's meaningful names which are easier to remember than IPs. For example my router has it's own domainname such as **router.local**. 

Having a DNS failover is very important, as I mentioned I often had troubles with just the one DNS. I solved this problem by installing PiHole on my second Pi Zero W. 

Fixing one problem gave me another one...


## Sync Settings between DNS Servers
Having two PiHoles and lots of DNS records and other settings became tedious work to keep up with when I was playing around with my tiny homelab and networking.
So I wrote a Bash Shell script.

![PiHole Local DNS](/images/posts/pihole-dns.png)

Using my script [PiHole Rsync - https://github.com/jejje/pihole-rsync](https://github.com/jejje/pihole-rsync) we can solve the problem of repetition. It setups up a simple cronjob to run itself every fifteen minutes. The script is using rsync to update the secondary server from the primary.

Download and make it executable
```shell
cd /etc/pihole/
wget https://raw.githubusercontent.com/jejje/pihole-rsync/main/pi_rsync.sh
chmod +x pi_rsync.sh
```

Setup these variables first
```shell
#### Setup Vars ####
# What files to RSYNC
SYNCFILES=(gravity.db custom.list dhcp.leases local.list) 
# The Secondary PiHole Host
HOST=192.168.0.114
# Username on Secondary HOST
USER=pi
# Password on Secondary HOST
PSW=rasberry
# Update interval for CRONJOB
CRONTIME=15
```

Run this command once to setup the cronjob, and it will run every 15 minutes.
```shell
./pi_rsync.sh -i
```

To run it manually and see that everything works
```shell
./pi_rsync.sh -s
```
Read more at [my Github](https://github.com/jejje/pihole-rsync)
## Simple Solutions are the Best
Every fifteen minutes all my changes to the primary DNS will propegate and I can sit back and surf the web ad free and use domain names for my local home network. I hope
