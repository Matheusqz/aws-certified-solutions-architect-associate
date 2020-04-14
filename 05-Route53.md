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

## Routing Policies Available on AWS

### Simple Routing

If you choose the simple routing policy you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route53 returns all values to the user in a random order.

### Weighted Routing

Allows you split your traffic based on different weights assigned. For example, you can set 10% of your traffic to go to US-EAST-1 and 90% to go to EU-WEST-1.

### Latency-based Routing

Allows you to route your traffic based on the lowest network latency for your end user (ie which region will give them the fastest response time).
To use latency-based routing, you create a latency resource record set fot the Amazon EC2 (or ELB) resource in each region that hosts your website. When Amazon Route53 receives a query for your site, it selects the latency resource record set fot the region that gives the user the lowest latency. Route53 then responds with the value associated with that resource record set. 

### Failover Routing

When a request is made, it can be a active host and a passive host, when the active host is down, Route53 will send the traffic to the passive host. 

### Geolocation Routing

Geolocation routing lets you choose where your traffic will be sent based on the geographic location of your users (ie the location from which DNS queries originate). For example, you might want all queries from Europe to be routed to a fleet of EC2 instances that are specifically configured for European customers. These servers may have the local language of your European customers and all prices are dispalyed in Euros.

### Geoproximity Answer Routing (Traffic Flow Only)

Geoproximity routing lets route53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, kbiwn as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource. To use geoproximity routing, you must use Route53 traffic flow.

### Multivalue Answer Routing

Multivalue answer routing lets you configure Route53 to return multiple values, such as IP addresses for your web server, in response to DNS queries. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources. This is similar to simple routing however it allows you to put health checks on each record set.

## Health Checks

- You can set health checks on individual record sets
- If a record set fails a health check it will be removed from Route53 until it passes the health check
- You can set SNS notifications to alaet you if a health check is failed

# Summary

- ELB do not have pre-defined IPv4 addresses, you resolve to them using a DNS name
- Undestand the difference between an alias Record and a CName (CName not a naked DNS)
- DNS types - SOA Records, NS Records, A Records, CName, MX Records, PTR Records
- Simple Routing Policy only one record with multiple IP addresses, if have multiple calues in a record, Route 53 returns all values in a random order. It cannot have a health check.
- Weighted Routing Policy - set weighted of traffic on a record, can have health check
- latency Routing Policy - check the latency of the request and give the record with the lowest latency 
- Failover Routing Policy - you can configured an active record and a passive, if the active go unhealth, the request is changed to the passive record
- Geolocation Routing Policy - made routing decision based on the location of que request
- Geoproximity Routing (for Traffic Flow Only) - special feature that routing your traffic based on the geographic location of your users and your resources. You can choose route more or less traffic by specifying a value (bias)
- Multivalue Answer Policy - same as Simple Routing Policy, but with health checks.
