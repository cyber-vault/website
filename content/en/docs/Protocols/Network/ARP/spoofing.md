---
title: "Spoofing"
linkTitle: "Spoofing"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "Spoofing ARP requests can change the routing of packets and is required for a Man in the middle attack." 
---
By spoofing the source adress of the ARP request it is possible to have the target accept the new address. This is due to the fact that ARP is stateless and there is no authentication. 

## Perform

There are tools and scripts that can perform arp spoofing.
One of the more well known framworks in python is named Scapy this framework is used  for packet manipulation is able to send ARP messages and craft frames from scratch.

### Arpspoof
using the kali tool arp spoof you can spoof a target adress and redirect traffic to a target of your choice. This tool is often used in combination with other tools to perform MiTM attacks on the network.

## Mitigation

There are several ways of mitigating ARP spoofing attacks

### Static ARP entries

The simplest way of mitigating this attack is to use static read only entries for critical services in the ARP cache. 

This mitigation can impose a lot of work for network maintenace. These static solutions do not scale on large networks.


### ARP Spoofing detection and prevention software
There is software on the market that can performs cross checks of  ARP responses based on the reponse the software is able to block the arp request. 

These options might be integrated with a DHCP server so that both static and dynamic adresses are verified. This capability might be intregrated into switches and routers.

#### AntiArp
this software provides windows based spoofing prevention at the kernel level

#### Arpstar
Arpstar is a linux module for kernel 2.6 and linksys routers that drops invalid packets that violate mapping and has a capability to re-poision (heal) ARP tables.

####  KVM 
KVM also provides a way to prevent MAC spoofing.

#### OpenBSD
OpenBSD passively watches for hosts impersonating the local host and sends a notification in case of an attempt to overwrite a permanent entry. 

#### OS security
Several Linux based operating systems have mitigations available to them. These methods are normally not enabled.
