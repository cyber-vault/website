---
title: "DHCP"
date: 2020-05-31T16:20:58+02:00
draft: false
description: "Dynamic Host Configuration Protocol is a protocol to handle the assignments of IPv4 adresses in a network." 
---
DHCP stands for Dynamic Host Configuration Protocol. This protocol is used to assign IP adresses on hosts (DHCP CLients). This reduces the manual effort that is required to configure clients on a network.

DHCP has replaced the older BOOTP system. From the client perspective DHCP is an extention of the BOOTP system this is how it retains compatibility with older clients.

One of the features of DHCP over the BOOTP protocol is the

DHCP servers can distribute any IP class on the basis of their netmask. There are 3 types of DHCP assignment. 
- Automatic Allocation: DHCP assigns a permanent IP address to a client.
- Manual Allocation: Client's IP address is assigned by the administrator, DHCP conveys the address to the client. 
- Dynamic Allocation : DHCP assigns an IP address to the client for a limited period of time (lease).

## Transport protocol
DHCP uses UDP as transport protocols. The client sends messages to the server on port 67 and the server sends messages to the client on UDP port 68. 

## High level Operation

The steps below show how an client obtains an IP adress.

1. DHCP Discover : DHCP client broadcasts a DHCP discover message to the DHCP server for an IP adress lease request through the subnet mask.
2. DHCP Offer: The DHCP server recieves DHCP Discover message for an IP address lease from DHCP client and reserves an IP for it. The server sends a DHCP Offer message to the DHCP client for IP lease. 
3. DHCP Request: DHCP client broadcasts a message to the DHCP server for acceptance of IP by recieving offered IP packets  and make DHCP request it's Ip configuration
4. DHCP Ackknowledgement: DHCP server receives the DHCP client request for IP cofngiuration process and responds with an DHCPACK message send to the client with the commited IP address and its configuration and with some  additional information like lease time.

Upon release of the address the following message gets send. 

- DHCP Release When a client lease time expires or the client leaves the network the client senda DHCP release packet to the DHCP server to release the adress.
 

## Low Level operation

The figure below shows the format of a DHCP message and it discribes each field of the message. The number in parentheses indicate the size of each field in octets.

```
 0                   1                   2                   3
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     op (1)    |   htype (1)   |   hlen (1)    |   hops (1)    |
   +---------------+---------------+---------------+---------------+
   |                            xid (4)                            |
   +-------------------------------+-------------------------------+
   |           secs (2)            |           flags (2)           |
   +-------------------------------+-------------------------------+
   |                          ciaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          yiaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          siaddr  (4)                          |
   +---------------------------------------------------------------+
   |                          giaddr  (4)                          |
   +---------------------------------------------------------------+
   |                                                               |
   |                          chaddr  (16)                         |
   |                                                               |
   |                                                               |
   +---------------------------------------------------------------+
   |                                                               |
   |                          sname   (64)                         |
   +---------------------------------------------------------------+
   |                                                               |
   |                          file    (128)                        |
   +---------------------------------------------------------------+
   |                                                               |
   |                          options (variable)                   |
   +---------------------------------------------------------------+
```

```
 FIELD      OCTETS       DESCRIPTION
   -----      ------       -----------

   op            1  Message op code / message type.
                    1 = BOOTREQUEST, 2 = BOOTREPLY
   htype         1  Hardware address type, see ARP section in "Assigned
                    Numbers" RFC; e.g., '1' = 10mb ethernet.
   hlen          1  Hardware address length (e.g.  '6' for 10mb
                    ethernet).
   hops          1  Client sets to zero, optionally used by relay agents
                    when booting via a relay agent.
   xid           4  Transaction ID, a random number chosen by the
                    client, used by the client and server to associate
                    messages and responses between a client and a
                    server.
   secs          2  Filled in by client, seconds elapsed since client
                    began address acquisition or renewal process.
   flags         2  Flags (see figure 2).
   ciaddr        4  Client IP address; only filled in if client is in
                    BOUND, RENEW or REBINDING state and can respond
                    to ARP requests.
   yiaddr        4  'your' (client) IP address.
   siaddr        4  IP address of next server to use in bootstrap;
                    returned in DHCPOFFER, DHCPACK by server.
   giaddr        4  Relay agent IP address, used in booting via a
                    relay agent.
   chaddr       16  Client hardware address.
   sname        64  Optional server host name, null terminated string.
   file        128  Boot file name, null terminated string; "generic"
                    name or null in DHCPDISCOVER, fully qualified
                    directory-path name in DHCPOFFER.
   options     var  Optional parameters field.  See the options
                    documents for a list of defined options.
```

The options fioeld is now a variable length with an minimum length of 312 octets. The DHCP client must be prepared to receive a message of upto 576 octets.


## References

https://tools.ietf.org/html/rfc2131
https://tools.ietf.org/html/rfc4388
https://tools.ietf.org/html/rfc1542

