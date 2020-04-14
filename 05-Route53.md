# Route53

the origin of the name comes from route 53 that crosses the USA and the service is at port 53.

## DNS Intro

DNS is used to convert human friendlyy domain names (http://acloud.guru) into an Internet Protocol (IP) address (such as http://82.124.53.1).
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

### Types of DNS Records

#### A Records

An "A" record is the fundamental type of DNS record. The "A" in A record stands for "Address". The A record is used by a computer to translate the name of the domain to an IP address. For example google.com might point to 123.12.12.2.

#### 

## Route53



# Summary

- 
