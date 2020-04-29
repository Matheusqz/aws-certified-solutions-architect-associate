# Virtual Private Cloud

## Introduction

Think of a VPC as a virtual data centre in the cloud. AWS VPC lets you provision a logically isolated section of the Amazon Web Services (AWS) Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own ip address range, creation of subnets and configuration of route tables and network gateways.

You can easily customize the network configuration for your Amazon Virtual Private Cloud. For example, you can create a puclic-facing subnet for your webservers that has access to the Internet and place your backend systems such as databases or application servers in a private-facing subnet with no Internet access. You can leverage multiple layers of security, including security groups and network access control lists, to help control access to Amazon EC2 instances in each subnet.

Additionally, you can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage the AWS cloud as an extension of your corporate datacenter.

### VPC Features

- Launch instances into a subnet of your choosing
- Assign custom IP address ranges in each subnet
- Configure route tables between subnets
- Create internet gateway and attach it to our VPC
- Much better security control over your AWS resources
- Instance security groups
- Subnet network access control list (ACLS)

### Default VPC vs Custom VPC

- Default VPC is user friendly, allowing you to immediately deploy instances
- All subnets in default VPC have a route out to the internet
- Each EC2 instance has both a public and private IP address.

### VPC Peering

- Allows you to connect one VPC with another via a direct network route using private IP addresses
- Instances behave as if they were on the same private network
- You can peer VPC's with other AWS accounts as well as with other VPC in the same account
- Perring is in star configuration: ie 1 central VPC peers with 4 others. NO TRANSITIVE PEERING!!
- You can peer between regions

### IMG VPC Puplic & Private

## Build a Custom VPC

## Network Address Translation (NAT)

### IMG NAT 

- When creating a NAT instance, Disable Source/Destination Check on the instance
- NAT instance must be in a public subnet
- There must be a route out of the private subnet to the NAT instance in order this to work
- The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.
- You can create high availability using Autoscaling Groups, multiple subnets in different AZs and a script to automate failover
- NAT instances are always behind a security group
- NAT instances are redundant inside the Availability Zone
- Preferred by the enterprise
- Starts at 5Gbps and scales currently to 45Gbps
- No need to patch
- Not associated with security groups
- Automatically assinged a public ip address
- Remember to update your route tables
- No need to disable Source/Destination Checks

### NAT Gateways

If you have resources in mutiple Availability Zones and they share one NAT gateway, in the event that the NAT gateway's AZ is down, resources in the others AZ lose internet access. To create an AZ-independent architecture , create a NAT gateway in each AZ and configure your routing to ensure that resources use the NAT gateway in the same AZ.

## Network Access Control Lists (ACL)

## Custom VPC and ELBs

## VPC Flow Logs

## Bastions

## Direct Connect

## Setting Up a VPN Over a Direct Connect Connection

## Global Accelerator

## VPC End Points

# Summary
