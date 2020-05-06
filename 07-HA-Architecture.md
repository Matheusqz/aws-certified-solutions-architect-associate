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

Classic Load Balancer routes each request independetly to the registered EC2 instance with the smallest load. Sticky sessions allow you bind a user's session to a specific EC2 instance. This ensures that all requsts from the user during the session are sent to the same instance. You can enable Stick Sessions for Application Load Balancers as well, but the traffic will be sent at the Target Group Level.

#### Cross Zone Load Balancing

The traffic can be acroos AZ to balance to all EC2.

#### Path Patterns

You can create a listener with rues to forward requests based on the URL path. This is known as path-based routing. If you are running microservices, you can route traffic to multiple back-end services using path-based routing. For example, you can route general requests to one target group and requests to render images to another target group.

## Autoscaling

### Components

#### Groups

Logical component, webserver group or application group or database group, etc.

#### Configuration Templates

Groups uses a launch template or a launch configuration as a configuration template for its EC2 instances. You can specify information sush as the AMI ID, instance type, key pair, security groups and block device mapping for your instances.

#### Scaling Options

Scaling optins provides several ways for to scale your auto scaling groups. For example, you can configure a group to scale based on the occurrence of specified conditions (dynamic scaling) or on a schedule.

## Scaling Options

### Maintain Current instance levels at all times

You can configure your Auto Scaling group to maintain a specified number of running instances at all times. To maintain the current instance levels, Amazon EC2 Auto Scaling performs a periodic health check on running instances within an Auto Scaling group. When Amazon EC2 Auto Scaling finds an unhealthy instance, it terminates that instance and launches a new one.

### Scale Manually

Manual scaling is the most basic way to scale your resources, where you specify only the change in the maximum, minimum or desired capacity of your Auto Scaling group.

### Scale based on a schedule

Scaling by schedule means that scaling actions are performed automatically as a function of time and date. This is useful when you know exacty when to increase or decrease the number of instances in your group, simply because the need arises on a predictable schedule.

### Scale based on demand

A more advanced way to scale your resources - using scaling policies, lets you define parameters that control the scaling process. For example, lets say that you have a web application that currently runs on two instances and you want the CPU utilization of the Auto Scaling group to stay at around 50% (percent) when the load on the application changes. This method is useful for scaling in respnse to changing conditions, when you don't know when those conditions will change. You can set up Amazon EC2 Auto Scaling to respond for you.

### Predictive Scaling

You can also use Amzon EC2 Auto Scaling in combination with AWS Auto Scaling to scale resources across multiple services. AWS Auto Scaling can help you maintain optimal availability and performance by combining predictive scaling and dynamic scaling (proactive and reactive approaches, respectively) to scale your Amzon EC2 capacity faster.

## HA Architecture

- Everthing fails. Everthing. You should plan for failure.
- Simian Army
- Use Multiple AZ and Multiple Regions where ever you can
- Know the diffence between Multi-AZ and Read Replicas for RDS
- Know the difference between scaling out and scaling up.
- Read the question carefully and always consider the cost element
- Know the differenc S3 storage classes.
- **IMG**

### HA Word Press Site

### Setting Up EC2

### Adding REslience and Autoscaling

### Cleaning Up

### CloudFormation

- Is a way of completely scripting your cloud environment
- Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly

### Elastic Beanstalk

With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications. You simply upload your application, and Elastic BeanStalk automatically handles the details of capacity provisioning, load balancing, scaling and health monitoring.


# Summary
