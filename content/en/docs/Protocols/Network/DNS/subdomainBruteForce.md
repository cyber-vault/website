---
title: "Subdomain Brute force"
linkTitle: "Subdomain Brute force"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "using wordlists its possible to discover unlistedsubdomains." 
---
It is possible to enumerate subdomains by brute forcing them by sending queries to the target name server and watching the  returns.

In the packet header there will be flags present that indicate teh stattus of the subdomain (if it is presesnt or not)

Subdomain brute forcing is often done with wordlists, scraped wordlists and sometimes done with direct brute forcing. 

This guesses the subdomain and looks for a reply.

## Low Level

The low level is simple. First a request is send to the subdomain if the response from the DNS server is a valid subdomain this you have found one then.

## Perform
We can use application like Gobuster to brute force with wordlists or feed wordlists to.

Amass we are able to get multiple types of information one of which is the a brute force for subdomain discovery.

## Mitigation
By using subdomains that are not in word lists it becomes a lot more difficult to brute force subdomains. e
