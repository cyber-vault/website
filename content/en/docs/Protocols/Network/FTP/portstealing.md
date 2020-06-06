---
title: "Port Stealing"
linkTitle: "Port Stealing"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "Port stealing allows an attacker to steal data that is requested from the FTP server" 
---
Data transfer within  the FTP protocol creates a new TCP connection for each file to be transported.  The client connects to this socket automatically. 

An attacker might be able to make a connection before the server-client connection.

## Low Level
There are preconditions required for hte 

### Preconditions
Since we have to guess thw port number we want to checkif the software sets the ports sequencaially. 

To get the port number we are at we can connect and use the PASV command. this will give us an indication of what ports are being used. 

The client side can be more difficult but it can be estimated that most operating systems are either just above 1024 or above 32000. 

Latency is important in this attack. Since it is a race condition you want as little latency between the  server and the attacker. While having as much latency as possible between the client and teh server.


## Perform
To perform the attack you need to port scan the ranges in which the FTP server opens ports.
This should be done with an connection scan. The data that is outputted need to be stored then and analyzed.


## Mitigations
This attack is hard to mitigate. This can be done either with custom written FTP software that warns of a a difference in connection.

Another mitigation is the user itself. If the user is aware of this vulnerability then a failure of recieving data is 

The attack can be detected by using tools that can detect connect() scanning.
