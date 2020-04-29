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

- Your VPC automatically comes with a default network ACL and by default it allows all outbound and inbound traffic
- You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
- Each subnet in your VPC must be associated with network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL
- Block IP addresses using network ACLs not Security Groups
- You can associate a network ACL with multiple subnets, however a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the precious association is removed.
- Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
- Network ACLs have separate inbound and outbound rules and each rule can either allow or deny traffic.
- Network ACLs are stateless, responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa)

## Custom VPC and ELBs

You need a least two public subnets to provide a load balancer

## VPC Flow Logs

VPC Flow Logs is a feature that enables you to capture information abount the IP traffic going to and from network interfaces in your VPC. Flow log data is stored using Amzon ClodWatch Logs. After you've created a flow log, you can view and retrieve its data in Amzon CloudWatch Logs.

- You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.
- You cannot tag flow log
- After you've created a flow log, you cannot change its configuration, for example, you can't associate a different IAM role with the flow log
- Not all IP traffic is monitored:
  - Traffic generated by instances when they contact the Amazon DNS server. If you use own DNS server, then all traffic to that DNS server is logged.
  - Traffic generated by windows instance for amazon Windows license activation
  - Traffic to and from 169.254.169.254 for instance metadata
  - DHCP traffic
  - Traffic to the reserved IP address for the default VPC router

## Bastions Host

A bastion host is special purpose computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single application, for example a proxy server, and all other services are removed or limited to reduce the threat to the computer. It is hardened in this manner primarily due to its location and purpose, which is either on the outside of a firewall or in a demilitarized (DMZ) and usually involves access from untrusted networks or computers.

### IMG Basiont in action

- A NAT Gateway or NAT instances is used to provide internet traffic to EC2 instances in a private subnets
- A Bastion is used to securely administer EC2 instances (Using SSH or RDP). Bastions are called Jump Boxes in Australia
- You cannot use a NAT Gateway as a Bastion host

## Direct Connect



## Setting Up a VPN Over a Direct Connect Connection

## Global Accelerator

## VPC End Points

# Summary
