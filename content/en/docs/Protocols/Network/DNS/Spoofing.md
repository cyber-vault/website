---
title: "Spoofing attack"
linkTitle: "Spoofing attack"
date: 2020-05-31T16:20:47+02:00
draft: true
description: "it is possbile to corrupt DNS servers using a spoofing attack." 
---
Also known als DNS poisioning this is an attack where currupt DNS data is introduced into the DNS resolvers cache causing the nameserver to return the wrong result.

DNS spoofing can be performed in 2 ways DNS server comprimise and MiTM.

When an attacker performs a MiTM on a on a client or DNS server then any query can be adjusted. When performed on a client This means that the interception allows for a redirect.

If this is performed on a DNS forwarder then the request from the forwarder to the root server should be intercepted. This allows you to modifiy requests as they come in from the forwarder. if these requests are modified then the entire forwarder has it now in its cache.

## low level

modifiying the DNS involves modifying the packets that are returned from the root server. These packets must have  their RDATA field adjusted to your comprimised server.

(untested)
if the response is changed to a CNAME (if this works) then it might be possible to redirect it to a fast flux domain.

## perform

There are tools like  dnsspoof that can perform dns spoofing. 

modifiying packets at the low level is a idea of mine and might not be possible this also needs to be tested and scripted.


## mitigation

One of the methods of mitigating this attack is to monitor the network for man in the middle attempts.

Hardcoded hosts for critical hosts (eg SSO, Google, Facebook, Corporate site etc.)

alerts on the dns server that can monitor gateways and route changes within the network.

