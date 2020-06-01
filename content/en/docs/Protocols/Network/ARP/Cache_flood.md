---
title: "Cache Flood"
linkTitle: "Cache Flood"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "Cache flooding is an attack that can flood the CAM table this causes a switch to switch to a HUB mode." 
---
It is possible to fill up the ARP cache table within a switch which can cause the switch to go into fail-safe mode. This is common with older switches that have limited hardware.

By flooding the switch swith spoofed ARP request and reply messages it is possible to fill up this table. 

If the ARP table of the switch is completely filled then the switch can no longer redirect traffic to the correct endpoints. Instead it will switch to fail-safe and will send the traffic to all ports. 

Effectively the attacker has turned the switch into a HUB with all the benefits of a switch (no packet collision). This allows an attacker to listen into all of the traffic that is transferred on the switch. 

## Low Level

When a request is send on FF:FF:FF:FF:FF a reply is send with a spoofed adress. To the adress that is sending the ARP broadcast. 

If this is performed fast enough (loads of times per second) the ARP cache MAY flood

## Perform

The tool macof which is part of the dsniff package can perform these floods. 

## Mitigation
Cisco swtiches have mitigation build in and newer swtiches can clear the cache fast enough to mitigate all but the most violent attacks.
