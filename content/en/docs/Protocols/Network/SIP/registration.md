---
title: "Registration Removal"
linkTitle: "Registration Removal"
date: 2020-05-31T16:20:47+02:00
draft: false
description: "Its possible to unregister a user " 
---
Registration removal attack is a signal manipulation attack. This attack will deregister a user on the network and will have as an effect that the user will no longer recieve messages from the SIP proxy. 


## Low level
By sending a custom made REGISTER request with the fields ```Contact``` and ```Expires``` The contact header is the actual adress taht the registrant is listening on for incomming calls. Expiration indicates how long it takes to expire. 

To remove a registration the attacker sends a modified header with the contact set to * and the expiration set to 0. This will unregister the user that requested the message. Ofcourse its possible to spoof messages.


## Perform
Send a crafted SIP packet with the following headers

```
Contact: *
Expire: 0
```


## Mitigation
It is possible to mitigate the attack by monitoring for the headers in the request.

