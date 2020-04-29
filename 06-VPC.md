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

- When you create a VPC a default Route Table, Network Access Control List (NACL) and a default Security Group are created automatically
- It won't create any subnets, nor will it create a default internet gateway
- AZ are randomized for each account
- Amazon always reserve 5 IP addesses within your subnets
- You can olny have 1 internet Gateway per VPC
- Secutiry groups can't span VPCs

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

AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS. Using AWS Direct Connect, you can establish private connectivity between AWS and your datacenter, office or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput and provide a more consistent network experience than internet-based connections.

- Direct Connect directly connects your data center to AWS
- Useful for high throughput workloads (ie lots of network traffic)
- Or if you need a stable and reliable secure connection

## Setting Up a VPN Over a Direct Connect Connection

- Create a virtual interface in the Direct Connect console. This is a public Virtual Interface
- Go to the VPC console and then to VPN connections. Create a customer Gateway
- Create a Virtual Private Gateway
- Attach the virtual private Gateway to the desired VPC
- Select VPN Connections and create new VPN Connection
- Select the Virtual Private Gateway and the Customer Gateway
- Once the VPN is available, set up the VPN on the customer gateway or firewall.

## Global Accelerator

AWS Global Accelerator is a service in which you create accelerators to improve availability and performance of your applications for local ana global users

Global Accelerator directs traffic to optimal endpoints over the AWS global network. This improves the availability and performance of your internet applications that are used a global audience.

### Components

#### Static IP addresses

By defafaul, Global Accelarator provides you with two static IP addresses that you associate with your accelerator. Alternatively, you can bring your own.

#### Accelerator

An accelerator directs traffic to optimal endpoints over the AWS global network to improve the availability and performance of your internet applications. Each accelerator includes one or more listeners

#### DNS Name

Global Accelerator assingns each accelerator a default Domain Name Systeam (DNS) name - similiar to a123456789abcdef.awsglobalaccelerator.com - that points to the static IP addresses that Global Accelerator assings to you.
Depending in the use case, you can use your accelerator static IP addresses or DNS name to route traffic to your accelerator or set up DNS records to route traffic using your own custom domain name.

#### Network Zone

A network zone services the static IP addresses for accelerator from a unique IP subnet. Similiar to an AWS AZ, a network zone is an isolated unit with its own set of physical infrastructure
When you configure an accelerator, by defaul, Global Accelerator allocates two IPv4 addresses for it. If one IP addresss from a network zone becomes unavailable due to IP address blockuing by certain cliente network or network disruptions, client applications can retry on the healthy static IP address from the other isolated network zone.

#### Listener

A listener processes inbound connections from clients to Global Accelerator, based on the port (or port range) and protocol that you configure. Global Accelerator suports both TCP and UDP protocols.
Each listerer has one or more endpoint groups associated with it, and traffic is forwarded to endpoints in one of the groups.
You associate endpoint groups with listerners by specifing the Regions that you want to distribute traffic to traffic is distributed to optimal endpoints within the endpoint groups associated with a listener.

#### Endpoint Group

Each endpoint group is associated with a specific AWS Region.
Endpoint groups include one or more endpoints in the Region.
You can increase or reduce the percentage of traffic that would be otherwise directed to an endpoint group by adjusting a setting called traffic dial.
The traffic dial lets you easily do performance testing or blue/green deployment testing for new releases across different AWS Regions, for example.

#### Endpoint

Endpoint can be Network Load Balacncers, Applications Load Balancers, EC2 instances or Elastic IP addressses.
An applications Load Balancer endpoint can be an internet-facing or internal. Traffic is routed to endpoints based on configuration options that you choose, such as endpoint weights.
For each endpoint, you can configure weights, which are numbres that you can use to specify the proportion of traffic to route to each one. This can be useful, for example, todo performance testing within a Region.

## VPC End Points

# Summary
