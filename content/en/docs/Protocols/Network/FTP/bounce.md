---
title: "Bounce Attack"
linkTitle: "Bounce Attack"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "A FTP bounce attack allows an attack er to misuse a opened FTP port." 
---
The FTP Bounce attack takes advantage of the PORT command that allows port requests. 

In a FTP Bounce attack this PORT request is done on another IP within the network. 
This allows an attacker to either bounce connections or to map the ports on the internal network.

This works because the protocol that FTP uses for its command channel is the Telnet protocol. 

## Low Level

- Attacker opens an FTP serssion to the victim.
- The attacker issues a PORT command and requests the port on another server instead of the vicim server. 
- The victim server the command over the port to the other server.
- When the other servre replies it sends the data back over the established connection.

https://www.linux.org/threads/nmap-ftp-bounce-attack.4493/



## Perform
This attack can be tested using nmap this is done with the -b flag for bounce.

An example is nmap -v -b email@domain target adress -Pn


## Mitigate
Almost all mondern FTP software has mitigations enabled that does not allow you to connect beyond your host.

Most servers can have settigns to disable. Check the googles for how to. 
