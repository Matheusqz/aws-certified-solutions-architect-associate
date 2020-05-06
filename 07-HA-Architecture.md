# HA Architecture

## Load Balancers

load balancing refers to the process of distributing a set of tasks over a set of resources (computing units, webserver), with the aim of making their overall processing more efficien.

### Types

#### Aplication Load Balancers

Best suited for load balancing of **HTTP and HTTPS traffic**. They operate at Layer 7 and are application-aware (can see insede the aplications, all request that you made, can made intelligent decision). They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

#### Network LoadBalancers

Best suited for load balancing of **TCP traffic** where extreme performance is required. Operating at the connection level (Layer 4), Network Load Balancer are capable of handing millions of requests per second, while maintaing ultra-low latencies. Use for extreme performance!

#### Classic LoadBalancers (legacy-cheaper)

You can load balance HTTP/HTTPS applications and use Layer 7-specific features, such as X-Forwaeded and sticky sessions. You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol.

### Erros in Load Balancing

If your application stops responding, the ELB responds with a 504 error (Gateway has timed out). This means that the application is having issues. This could be either at the Web Server layer or at the Database Layer. Identify where the application is failing and scale it up or out where possible.

### X-Forwarded-For Header

Get the IPv4 address of your end user at your application.

### Health Checks

Instances are monitored by ELB are reported as:
  - InService
  - OutofService
Health Checks see if the instance health by talking to it.
Load Balances have theis own DNS name. You are never given an IP address.

### Advanced Load Balancer

#### Sticky Sessions

## Autoscaling

### Autoscaling Groups Lab

## HA Architecture

### HA Word Press Site

### Setting Up EC2

### Adding REslience and Autoscaling

### Cleaning Up

### CloudFormation

### Elastic Beanstalk

# Summary
