
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


![asg](https://user-images.githubusercontent.com/110176257/187237566-351336f1-87f0-4b31-ba89-6aff95aa400a.png)

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


## Creating an Auto Scaling group with an Application Load Balancer

From the AWS EC2 dashboard, select **Auto Scaling groups** at the bottom of left side of the page

![image](https://user-images.githubusercontent.com/110176257/187243248-9179cf98-b913-48f1-a575-d224fb643ecf.png)


- Name your ASG and select template instance

![image](https://user-images.githubusercontent.com/110176257/187243705-f08ee098-6711-4760-890b-d26a6fdd83bb.png)

- Select VPC and multiple subnets for high availability 

![image](https://user-images.githubusercontent.com/110176257/187244301-22f27139-acb4-45d9-bea1-d12e002d1b26.png)

- Configure load balancer

![image](https://user-images.githubusercontent.com/110176257/187244496-2d3ff623-04f9-40f3-9ad8-c7b5e71675a3.png)

- We use an ALB (because our application uses HTTP protocol) and internet facing load balancer, so that our app is globally available.

![image](https://user-images.githubusercontent.com/110176257/187244745-df1eb167-f9b9-4109-9697-0eba53d4498d.png)

- Create new target group or use existing

- Determine group size and scaling policy

![image](https://user-images.githubusercontent.com/110176257/187245331-4b7ba0f4-908a-4813-b943-dba30c584cbb.png)


- Add name tag to name EC2 instances

![image](https://user-images.githubusercontent.com/110176257/187246161-4dc8443b-1a61-48bd-b549-c1268518c502.png)


- Select **create auto scaling group**

![image](https://user-images.githubusercontent.com/110176257/187246278-e26fe872-39cf-4ef2-bfac-a231405ed8a9.png)

