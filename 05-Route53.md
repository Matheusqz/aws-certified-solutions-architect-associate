# Route53

the origin of the name comes from route 53 that crosses the USA and the service is at port 53.

## DNS Intro

DNS is used to convert human friendlyy domain names (acloud.guru) into an Internet Protocol (IP) address (such as 82.124.53.1).
IP Addresses are used by conputers to identify each other on the network. IP addresses commonly come in 2 different forms, IPv4  and IPv6.

### Top Level Domains

If we look at common domain names such as google.com, you will notice a string of characters separated by dots (periods). The last word in a domain name represents the "top level domain". The second word in a comain name is known as a second level domain name (this is optional though and depends on the domain name).
This top level domain names are controlled by the Internet Assinged Numbers Authority (IANA) in a root zone databases which is essentially a database of all available top level domains.
Because all of the names in a given domain name have to be unique there needs to be a way to organize this all so that domain names aren't doplicated. This is where domain registrars come in. A registrar is an authority that can assing domain names directly under one or more top-level domains. These domains are registered with interNIC, a service of ICANN, which enforces uniquesess domain names across the internet. Each domain name becomes registered in a central database known as the WhoIs database.

### Start of Authotiry (SOA) Record

The SOA record stores information about:
- The name of the server that supplied the data for the zone
- The administrator of the zone
- The current version of the data file
- The default number of seconds for the time-to-live file on resource records

### Name Server (NS) Records

Ther are used by Top level domain server to direct traffic to the content DNS server whith contains the authoritative DNS records.

Request -> Top Level Domain Server (.com) -> NS Record -> SOA Record (thet have the DNS record for the request)

#### Time to Live (TTL)

The lenght that a DNS record is cached on either the resolving Server or the users own local PC is equal to the value of the TTL in seconds. The lower TTL, the fast changes to DNS records take to propagate throughut the internet.

### Types of DNS Records

#### A Records

An "A" record is the fundamental type of DNS record. The "A" in A record stands for "Address". The A record is used by a computer to translate the name of the domain to an IP address. For example google.com might point to 123.12.12.2.

#### Canonical NAME (CName)

CName can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name m.acloud.guru that used for when users broese to your domain name on their mobile devices. You may also want the name mobile.acloud.guru to resolve to this same address.

#### Alias Records

Alisas records are used to map record sets in your hosted zone to Elastic Load Balancers, CloudFront distributions or S3 buckets that are configured as websites.
Alias records work like a CNAME record in that you can map one DNS name to another target DNS name.

##### Difference between an Alias Record and CNAME

- Alias record can be naked domain name, without the 
- CName can not be a naked domain name.
PS: Always prefer create a Alias Record over a CName

## Route53



# Summary

- 
