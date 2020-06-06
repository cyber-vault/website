---
title: "SIP"
date: 2020-05-31T16:20:58+02:00
draft: false
description: "The Simple Message protocol is often used to establish telecommunications for example VoIP." 
---

Simple message Protocol is a protocol used in control of multimedia communications. Through SIP existing calls can be modified. SIP is not the actual protocol used for voice or video transmission. This is commonly Realtime Transport Protocol (RTP) or the secure variant Secue Realtime Transport Protocol (SRTP).

All resrouces in a SIP network has an Uniform Resource Identifier (URI) It follows the same syntax as in web services and email. SIP uses headers, encoding rules and status codes similar to HTTP.

a SIP proxy is often used to proxy connections to switching centers. Proxy servers are  able to 

SIP based telephony commonly implements a special version of the Signaling System 7 (SS7).
SS7 is commonly used as protcol between switching centers. 


## Transport protocol
Typicially port 5060 and 5061 are used with UDP, TCP and SCTP.
Commonly port 5060 uses the unencrypted format and port 5061 uses the encrypted format.

## High level
The sip protocol is a complicated protocol with a lot of sections to the protocol. For this reason the high / low level are different then normal and split into sections.

### Registration
When a user registers to a sip proxy it is possible that it requires a username and password. This password is send encrypted to the proxy server.

### starting a session (same proxy)
When a caller wants to start a session with another user on the same proxy. The user sends a message directly to the other user. When the other user accepts the call an RTP session is established bewteen the parties.  When the caller hangs up the callee gets an end pessage signal

# Low level
The low level has similar sections as the high level

### Registration
When a user sends the REGISTER flag to the proxy it sends a challange to the user. 
The user responds with his username and password this is encrypted with the challange and send to the proxy. If the authentication was succesfull the Proxy sends a 200 OK and the contact list to the user and assigns a Adress Of Record (AOR)

```

  Client                        SIP Server
     |                               |
     |          REGISTER F1          |
     |------------------------------>|
     |      401 Unauthorized F2      |
     |<------------------------------|
     |          REGISTER F3          |
     |------------------------------>|
     |            200 OK F4          |
     |<------------------------------|
     |                               |
```

### Starting a session
When user A starts a session he sends an F1 INVITE to user B. This causes device B to send a F2 RINGING back to user A.

If user B picks up the device the F3 200 OK is send to user A. This will trigger a ACK if the packet has been acknowledged.

When the ACK is recieved by user B the a RTP session is established between the users. 

When user B hangs up a 200 OK is returned by user A to indicate the end of the session
```
	 A                        B
     |                        |
     |       INVITE F1        |
     |----------------------->|
     |    180 Ringing F2      |
     |<-----------------------|
     |                        |
     |       200 OK F3        |
     |<-----------------------|
     |         ACK F4         |
     |----------------------->|
     |   Both Way RTP Media   |
     |<======================>|
     |                        |
     |         BYE F5         |
     |<-----------------------|
     |       200 OK F6        |
     |----------------------->|
     |                        |

```


# references
https://tools.ietf.org/html/rfc3665
https://tools.ietf.org/html/rfc3261
https://en.wikipedia.org/wiki/Session_Initiation_Protocol

