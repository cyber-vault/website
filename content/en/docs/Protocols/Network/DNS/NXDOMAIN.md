---
title: "NXDOMAIN attack"
linkTitle: "NXDOMAIN attack"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "An denial of service attack that can be used to exhaust the resources on the DNS server." 
---
The NXDOMAIN Attack is  Denial of service attacck where an attacker sends mass request for records that are either invalid or do not exist. This will consume resources on the server causing a slow down in lookups by valid clients. 

Often this flood request is intercepted by a proxy server which then takes the load and goes down or slows down the speed of resolving requests.

On stand alone DNS servers this is still a viable attack method to make dns servers unreachable. 

## Low Level

Sending MXDOMAIN requests to a server without MX domains causes floods choose a type of request you want to make and start requesting it with many bots aka standard flood fun fun. 

## Perform
This can be done by requesting a request packet with scapy.

## mitigation 
There are several options to mitigate this attack. One of the most common options is that the domain his blackholed so all requests for the domain are dropped. 

