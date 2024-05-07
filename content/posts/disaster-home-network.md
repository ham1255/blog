+++ 
draft = false
date = 2024-05-08T02:00:00+04:00
title = "Disaster home network to a Better one"
tags = ["OpenWrt", "Linux"]
categories = ["Networking", "Open-source"]
+++
How 8 years of me learning about stuff made a disaster home network, and how i did fix it.

*I kinda wana partially blame it on etisalat*

Note: *This post won't show you any technical stuff, as i will share in a later post in [tutorials](/tutorials).*
### Timeline:

* 2015:
    * etisalat Elife was installed 20mbps package
    * was covering one room

* 2016 Jan -> April:
    * Ethernet was connected to my/brother room 
    * Etisalat upgraded base package to 50mbps
* 2016 between may -> dec:
    * Huwaii router was installed on upstairs living room by *14 years old me :/*
    * Etisalat upgraded everone temporarly on for national days to end of the year to 100mbps
* 2017 -> 2019: 
    * i am not sure when etisalat made 500mbps base package for everyone
    * 1 extender was installed to help internet reach some rooms
* 2020: 
    * Tp-link router was installed into my other siblings room
    * i moved into my own room which means extra ethernet cable
* 2021:
    * tp-link router os was replaced to openwrt and was setup as a bridge

* 2022 -> 2023: nothing 

### Network diagram:

* if i interrupted etisalat agreement correctly, The GPON modem is etisalat property and we can't change and control it.
* Rooms placements in diagram is kinda weird.
* extenders were not included since they are considered wifi devices.

![](/images/posts/disaster-home-network/home_network.1.png)

`using draw.io`

### ISSUES i needed to solve:
* Wifi wasn't covering whole house.
* Bad wifi extenders that overheat to the point it drops packets 
* Wifi got so bad that each room got it own ssid ._.
* Double nated, broken ipv6.
* Main router was not 100% controllable / Running outdated software.
* Contractor scammed my father during house being built by not wiring the house ethernet into sockets But wires are still there.
* ethernet sockets were wired incorrectly *does not follow any code* but they work somehow. in the connected sockets At least


# The attempt to solve it:

I began researhing routers that can run openwrt for reasonable price

My eye fell on `TP-Link Archer C6 v2`, on box is said it supports wifi speeds up to 867mbps *which discovered as lie later*, so i ordered 5 routers for 600~ aed, also some extra stuff ethernet cat6 keystones and sockets. Which i had before.

now after i got everything i started to check etisalat provided router if it has openwrt firmware which is
`D-Link DIR-853 A3` it turned out it has firmware but in SNAPSHOTS as it was supported recently.

But there is roadblock. Etisalat....

I had to contact them, to disable a thing called `PLUG and Play` which basically you connect a router if provided by etisalat that automaticlly setup itself with pppoe username / password.

The reason i called it roadblock because on r/Dubai subreddit i saw people complaining so much that they can't replace router Due etisalat customer service refusing etc. i even laughed so hard when i saw this [post](https://www.reddit.com/r/dubai/comments/v59y6h/2022_guide_how_to_change_etisalat_router/) on reddit, it basically shows how bad d-link software can be. anyways, after i sorted out p&p with my father as connection under his name, and got the new pppoe username / password.

days later i started the upgrade on dlink router and oh man i thought i bricked it. since openwrt page for dlink router said that recovery option was broken, but it turned out that snapshot versions of openwrt does not ship luci the gui for openwrt, so i had to get spare router to use pppoe connection and to install luci using ssh, but some would say *why didn't use uci while in ssh?* because lmao, i had 15 mins to get the internet back.

after finishing up the router with openwrt and disabling wifi etc, i noticed something bad with speeds
They were bad, Because it turned out that dlink router ships hardware nat that can be enabled in the firewall, after testing it seems all great, now we begin installing the wifi access around the house.


### WiFi access points:

Like i said above, i have five routers of `TP-Link Archer C6 v2` which i setup as access point

which i placed on:
* Kitchen
* Siblings room
* upstairs living room
* downstairs majlis *not kinda used unless parties etc*
* one in my room for testing / backup reasons

configuration on all of these are bridged to main router which provides dhcp etc..

after setting up same ssid on them and enabling wifi roaming which now means moving around the house and phone switches the to close wifi access point.
also i had to deal with the kitchen and majlis because they habe sockets that either broken or not wired at all, which why i had to get 2 sockets 4 keystone ethernet and wire them in the right way. since i had equipment to detect which cable they are it was kinda easy but a time consuimg process.

after everything was setup wise, i basically had to install 8 port switch to for increasing number of ethernet, which i had from way before.


# Results:

* Wifi coverage got way better and somehow accesable from outside the house.
* Wifi roaming was working probably. *my mother loved it*
* no more double nat.
* each openwrt device can be customized when needed.
* Better ipv4 dhcp settings


# thoughts:

Why wifi routers are soo locked down? shouldn't user be able to control the router as they wish?
this evil crops locking down stuff to the point we don't own a thing.


# resources

https://openwrt.org/

https://firmware-selector.openwrt.org/

https://openwrt.org/docs/guide-quick-start/developmentinstallation