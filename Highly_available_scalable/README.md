
# Autoscaling and load balancers
##### Autoscaling groups and load balancers are tools to make your services highly available and highly scalable

![autoscale](https://user-images.githubusercontent.com/110176257/186621465-0ec3383c-4e3f-4584-bbe6-02396965e883.png)

## Scalability
Scalability in the context of cloud computing refers to the extent to which IT resources can be increased or decreased as needed to meet demand.

Scalability is one of the key benefits of cloud computing, it allows you to easily rent more resources from the cloud provider when its neccesary in real time, and automatically scale that down not when demand is low. This is incredibly cost efficient as demand is typically dynamic and unstable, this therefore saves you the need to spend a fortune to build a system capable of handling high demand, when most of the time it would only use a small fraction of its resources. By having these resources scalable on the cloud instead you only pay for that capability when you really need it.

Highly scalable systems are made very accessible in AWS through the use of **Auto Scaling groups**

### Auto Scaling groups
An Auto Scaling group in AWS is a collection of EC2 instances which are treated as a logical collection for management and scaling purposes, they use Amazon's Auto Scaling service to set **scaling policies**, min/max number of instances and health checks.

Auto scaling groups work by having a predetermined number of instances configured as the desired minimum capacity, and a scaling policy to determine when more resources/instances are needed to ensure high availability and handle more traffic.

Three main types of **scaling policy** are:
- Simple policy (e.g when CPU utilisation hits 80%, increase capacity by 50%)
- Step policy (e.g create 1 more instance when CPU at 40%, create another 2 when at 60%)
- Target tracking policy (following a specified load metric(eg. CPU always at 20%))

Auto Scaling groups can span multiple availability zones in a region (e.g eu-west-1a, eu-west-1b, eu-west-1c). This helps to ensure high availability because it means that one AZ going down wont be a **single point of failure** in your system.

## High availability 
high availability is defined as the capability of a system to operate without failing for an extended period of time. High availability of cloud based services is critical to their benefit over locally hosted servers, as without it they would be too unreliable.

Highly available systems can be created in a variety of ways, but typically follow these thtree principles:

- **Single point of failure**:
Any single points of failure should be identified and made reduntant or entirely avoided

- **Reliable crossover**:
Redundant systems are very important and common practise, it enables a backup component to take over for a failed one. It is important to make sure that when a failure does happen, the crossover to the backup system is reliable and automatic without losing data or affecting performance in a significant way.

- **Failure detectability**:
Systems must be monitored in order to detect failures, ideally with alert management configured so that most common failures have automated machanisms to handle the failure on their own. 

High availability is important because of the many critical systems that will have a severe impact on a business and/or people's lives if they fall below an operational thershhold.

High availability is often established via load balaning. When many users access a system, the many requests can flood and confuse the servers and cause failures and low performance. Load balancers become the single point of contact for users and automatically order and distribute workloads to servers. 

## Load balancers

A load balancer is the single point of contact for client requests. It can distribute incoming traffic across multiple EC2 instances, and across multiple Availability Zones.

There are three types of Load Balancer that AWS provides:

- ALB (application load balancer)
The application load balancer works on the seventh (HTTP/HTTPS) layer, it supports routing of traffic based on a wide range of request attributes (port number, host name, IP, HTTP method, etc)

- NLB (network load balancer)
The network load balancer routes traffic at the fourth (TCP) layer and routes traffic basedon TCP packet data. It has a very high performance and is typically used when your application does not use HTTP protocols. It works at ports specified in the listener configuration.

- ELB (elastic load balancer)
The elastic load balancer works at both layer 4 (TCP) and 7 (HTTP) and is the only load balancer that works in EC2-Classic. It was released before the ALB and NLB, and supports less features, it is therefore mainly used in legacy systems with EC2-classic instances.


