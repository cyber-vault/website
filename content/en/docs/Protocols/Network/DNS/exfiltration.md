---
title: "Exfiltration via DNS"
linkTitle: "Exfiltration via DNS"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "Exfiltration via DNS is relatively common in red team operations." 
---
It is possible to exfiltrate DNS using normal DNS queries. The content of the query and the targeted DNS server must be set manually (by the attacker) but it allows data to be used in the packet for exfiltration.

The intresting thing is that there are no extra network settings required or any wierdness going on in the network. It is just a DNS request to the DNS server

## Low level
it is possible to add extra information in either the options field or the QNAME field. 

The way to perform this attack is to use a real domain name but with an custom subdomain. The subdomain is the actual data that needs to be transferred to the attacker.

This causes the root server to contact the attacker name server. This nameserver will return some garbage information or commands to the victim machine.
All while looking and reacting like a normal DNS server for anyone out there. 

## Perform
This is out of the scope of this document.


## Mitigate

The best way to detect the possibility of exfiltration is by monitoring the requests from clients to the DNS server.
Since the data can be hidden in a lot of places in the packet deep packet inspection might be needed.

Another way to detect it is to monitor for frequent connections to suspicious domains.

