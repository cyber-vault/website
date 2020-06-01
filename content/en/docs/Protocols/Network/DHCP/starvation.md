---
title: "Starvation Attack"
linkTitle: "Starvation Attack"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "It is possible to exhaust DHCP adresses within a network by sending malicious request." 
---
This attack is catagorized as **DENIAL OF SERVICE**

This attack revolves about depleting the possible addresses that are available in the network. If there are no adresses avaialble new clients on the network  do not get an ip assigned. 

The way it is performed is by spoofing mac adresses on the network and performing an DHCP request with each spoofed MAC address.

An attack like this can be performed using a variaty of tools.
Yersi

## Low level
The way this attack works is by sending DHCP request messages and changing the chaddr field for each request performed. 
In the DHCP section you can find the exact packet breakdown in the Low level operation.

## Perform

The attack can be performed using a simple python script using the scapy library. There are also pre generated tools to perform this attack. The L2 attack framework Yersinia is one of these  tools.
## Mitigation

It is possible to mitigate the attack if the DHCP requests are being monitored. This makes it trivial for this attack to be discovered.

