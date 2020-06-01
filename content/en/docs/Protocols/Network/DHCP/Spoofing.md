---
title: "Spoofing Attack"
linkTitle: "Spoofing Attack"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "By sending spoofed messages it is possible to reconfigure DHCP clients." 
---
By spoofing the DHCP server it is possible to take over sending out IP configuration to clients from the real DHCP server.

This allows an attacker to set the gateway  or DNS of the client to a system under his control to perform man in the middle attacks. 

This attack can only be performed after a DHCP exhaustion attack has depleted the ip pool of the DHCP server. Or if the rogue DHCP server is able to reply to DHCP requests before the real server can respond the client ignores the request that arrives second.


## Low Level

This attack works the same as a normal DHCP request. The lack of IP's that are handed out after an exhaustion attack will prevent dhcp server fights.

Do not use the same IP range as  the server gives out this will cause massive conflicts and fights on the dhcp server. 


## Perform 


## References

