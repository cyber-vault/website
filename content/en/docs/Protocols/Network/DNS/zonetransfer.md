---
title: "Zone transfer"
linkTitle: "Zone transfer"
date: 2020-05-31T16:24:44+02:00
draft: false
---

The DNS zone transfer attack also known as AXFR attack because of the query that is usually performed.

This attack takes advantage of one of the many ways that administrators can syncronize their primary name server to the secondary name server. 

when a client sends a specially crafter message to the DNS server containing the AXFR flags If the primary server is misconfigured it will send an entire copy of the zone record to the requester. 
This may display the topology of the entire zone

## Low Level

The client sends a query with the opcode 0 with the special query type of 252 over the TCP  connection to the server. this will return the zone information if the server is misconfigured


## Perform

You can perfom zone transfers using the tool named dig.
```
dig axfr @dns-server domain.name
```
replace dns-server with authorative dns server


## Mitigation

Configure the DNS server to only respond to zone transfers from authenticated IP adresses. The instructions for this are in the manual of any DNS product.
