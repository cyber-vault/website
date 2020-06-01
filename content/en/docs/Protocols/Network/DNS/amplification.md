---
title: "Amplification Attack"
linkTitle: "Amplification Attack"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "A DNS fast flux attack is an way to prevent blocking by firewalls. This is usually used by black hats." 
---
Fast flux is a DNS technique that is used by attackers to try to evade blacklisting or discovery.

It does this by using a domain name with a large number of ip hosts assigned to it. These hosts rotate at a very short TTL (usually less then 5 minnutes) to evade capture. 

These are sometimes used by command and control servers, phising servers . This means that is becomes hard to discover because of a constant switching IP behind the domain.

Usuaully these IP lists are very large, sometimes thousands of IP adresses. The largest discovered so far has over 900k IP adresses.

Usually the machines that are accessed through the domain are just victim machines that are setup as forwarders. 

## Low Level

A large list of assigned IP adresses are stored on the DNS server. This is then switched at a high rate. For example 5 minutes( 300 seconds ) TTL on it. This means that the domain gets reassigned every 5 minutes. 

The TTL forces a message to be send to the root server.

## Perfrom
Setup a DNS server with low TTL and a large list of IP's in a round robin fasion. Each of the nameserver providers have different gui and abilities. Depending on the Nameserver provider it might be required to run an DNS server and have the domain name refer to it. 

the DNS server should be configured to use and large list of IP's to switch between. This might require special scripts to switch the IP in the configuration and restart the service.

Using the cloud this can be performed relatively easy. The price is on the other hand is high. This is due that since you need to switch between IPs and there is a minimum cost associated with it.  Furthermore this will definately get you banned from your cloud provider.

## Mitigation

The best way to mitigate this is by running a local DNS forwarder that keeps logs of all domains and associated IP adresses. 

A monitoring alert must be put in place to see if there are domains that have IPs assigned to them that might be suspicious. Suspicious IPs are for example consumer IP ranges and unexpected geological locations.

If an alert is triggered on an domain the DNS forwarder should block the DNS request to the hostname.
