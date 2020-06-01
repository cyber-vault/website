---
title: "DNS"
linkTitle: "DNS" 
date: 2020-05-31T16:07:40+02:00
draft: true
description: "Domain Name Services translate hostnames to IPs"
---

Domain Name System (DNS) is a naming system for computers,services, or other resources connnected to a network.
DNS is best known for translating domain names to IP addresses. DNS is ofcourse also able to do the reverse.

The DNS server can contain many different types of entries for domains. The most common ones that you will encounter are listed below:

- SOA : Start of Authority
- A and AAAA : IP Adress
- MX : SMTP mail exchanges
- NS : Name servers
- PTR : Reverse DNS lookups
- CNAME : Domain name aliases
- RP : ressponible person (dnssec?)
- RBL : Realtime blackhole list (anti spam)
- TXT: this record is used for various purposes but mainly seen in DKIM, DMARC and SPF Records.

### SOA Record
Normally DNS name servers are setup in clusters to ensure redundancy. The database of each of these clusters is syncronized through zone transfers. The SOA record contains data to control the zone transfer within the zone. The data that is required is the serial numer and different timespans. 

Without this record your domain name does not function nor comply with RFC1035. There are values assigned within the SOA record it these values have properties assigned to them below is the list of values and their properties:

- NAME: name of the zone
- IN: zone class (usually IN for internet)
- SOA: aberviviation for Start of Authority
- MNAME: Primary master name server for this zone. 
        - Update Requests should be forwarded towards the primary master
        - NOTIFY requests propagate outward from the primary master. 
- RNAME: email adress of the administrator responsible for this zone. (encoded as follows: part of the email adres before the @ becomes teh first label of the name the part after the @ the second part of the label. thus joe.test@example.com ```joe\.test.example.com```)
- SERIAL: serial number for this zone. If a secondary name server slaved to this one observes an increase in the numer it will assume the zone has been updated and initiate a zone transfer. 
- REFRESH: Number of seconds  after which the secondary name server should query the master server (recommendation 24 hours)
- RETRY: numbner of seconds after which secondary names servers should retry query the master server for the record to detect zone changes.(recommendation 2 hours for small zones)
- EXPIRE : number of seconds after which the secondary name server should stop answering request for this zone if the master does not respond. (Value must be bigger then REFRESH + RETRY) (Recommendation 1000 hours for small zones)
- TTL: Time to live for negative cahcing. Recommendation for small and stable zones is 2 days
- 

#### A and AAAA Record
A and AAAA records are used to point to an IP adress. This can be an internal or exteral adress. Hostnames are not accepted in this field. 

AAAA records are used exclusively for IPv6 adresses. The main difference between the A record and the AAAA record is the size of data it can hold. IPv4 is 32 bit and IPv6 is 128 bit. This is the reason for the naming scheme 4 times the size of the A record. 

#### MX record
The MX record is used to point to a mail server hostname or IP. The MX record can  take the optional value named PRIORITY this allows multiple MX records to be entered and a priority value to be assigned to it. The higher the priority value the later it is in the queue. 

#### NS Record
The NS record holds the IP adresses or hostnames of the authorotative name servers. There can be multiple name servers assigned within one zone.

#### PTR  record
A PTR record contains the ip adress or part of the IP adress that the pointer is refering to. a pointer will always return ```<IP>.in-addr.arpa```

#### CNAME Record
The CNAME record is an alias for a host. This measn that hosts and IPs can be set as its value

#### RP name
Responsible person name is an email adress in a format and i think its used for dnssec

#### RBL Record
Realtime Black hole List Contains a list of IP's who's accounts have been black listed from sending mails. Email servers can read these lists and blacklist emails in this manner. These lists are highly contriversal and are concidered the same as censorship. Still a lot of mail operators still use these servers.

#### TXT Record
Text records are used to send extra information that is used by other applications. This is one of the fields that needs to be set for DKIM email security features. 

## Transport protocol
DNS uses port 53 with the UDP protocol.

## High level operation
We want to go to ```subdomain.example.com```

The client sends a DNS request to the local dns server that it has configured. For the full domain. if the dns server knows the domain it returns it if not it queries one of the global root servers  For the ip Adresss of the .com dns servers.

It returns the IP for the .com and then it queries the servers for the .com zone and gets the IP for that zone. After querying the .com for example it returns that IP

Then finally the nameserver for teh example.com domain willl return the IP for subdomain.example.com. 


## Low level operation

Discribed below are the request and response that is send and recieved from the client. 
The packet contains the following:
 
1. Header
2. Question
3. Answer
4. Authority
5. Additional

#### Header


```

                                           1  1  1  1  1  1
             0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |                      ID                       |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |QR|   Opcode  |AA|TC|RD|RA| Z|AD|CD|   RCODE   |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |                QDCOUNT/ZOCOUNT                |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |                ANCOUNT/PRCOUNT                |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |                NSCOUNT/UPCOUNT                |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
            |                    ARCOUNT                    |
            +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+

```
 This is the header that is send to the client. 

Lets identify each of the fields in the p

- ID : 16 bit identifier that is assigned by the program that generated the query this is used by the requester to match replies with outstanding queries.
- QR: A one bit field that specifies whether the message is a query (0) or a response(1)
- OPCODE: a 4 bit field that specifies the type of query in this message (0 is a standard query)
- AA: Authoritative Answer. This bit is only meaningful in responses and speciefies that the response is an authoroty for the domain name server in question(you can use this bit to record wheter teh response is authorotative)
- TC: Truncation this specifies that the message is truncated.
- RD: Recursion desired This bit directs the name server to pursue the query recursively.
- RA: Recursion Available This is set or cleared in a response and denotes wheter recurseive query support is available in the name server.
- Z this bit is reserved for future use.
- RCODE: Response code This 4 bit field is set as part of the response The following values are possible:
    
    0. No error condition
    1. Format error: The name server was unable to iterpet the query
    2. Server Failure - the name serer was unable to process this query due to a problem with the name server
    3. Name Error - Meaningful only for responses from an authoritative name server, this code signals that the domain name in the query does not exist.
    4. Not implemented - the name server tdoes not support this kind of query
    5. Refused - the name server refuses to perform the sepcified operation for policy reasons.
- QDCOUNT : An 16 bit integer specifying the number of entries in the question section
- ADCOUNT: an 16 bit integer specifying the number of resource records in the answers section.
- NSCOUNT: 16 integer specifying the number of the name sever resource records in the authority section.
- ARCOUNT : an 16 bit integer specifiying the nuymber of resources in the record section.
- 

#### Request (Question)

  ```
                                 1  1  1  1  1  1
           0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                                               |
         /                                               /
         /                      QNAME                     /
         |                                               |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                      QTYPE                     |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                     QCLASS                     |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
  ```
  
- QNAME : A domain name represent as a sequence of labels, where each label consists of a length octet followed by that number of octet. The domain name terminates with the zero length octet for the null label of the root.
- QTYPE : A two octet code which specifies the type of the query (example 0x000f for MX records)
- QCLASS : a two octet code that specified the class of the query.

#### Response (Answer)
```
                                 1  1  1  1  1  1
           0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                                               |
         /                                               /
         /                      NAME                     /
         |                                               |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                      TYPE                     |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                     CLASS                     |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                      TTL                      |
         |                                               |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
         |                   RDLENGTH                    |
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--|
         /                     RDATA                     /
         /                                               /
         +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+

```
- NAME the domain name that was queried in the same format as teh QNAME in the question
- TYPE : 2 octet containing of the type codes and its specifies the meaning of data in the RDATA field.
- CLASS : Two octets which specify the class of the data in RDATA field.
- TTL : Number of seconds the results can be cached.
- RDLENGTH : The length of the RDATA field
- RDATA : The data of the response format is dependent on the TYPE field if the type is 0x0001 for  A records then it is the IP adress (4 octets) if it is a CNAME (0x0005) then it is the name of the alias etc.

## References

https://tools.ietf.org/html/rfc2929
https://www2.cs.duke.edu/courses/fall16/compsci356/DNS/DNS-primer.pdf
https://tools.ietf.org/html/rfc1035

