# Virtual Private Cloud (VPC)

Virtual Private Cloud on AWS is a service which allows users to launch AWS resources into a user-defined virtual network.
It is logically isolated from other virtual networks in the AWS Cloud.

![vpc](https://user-images.githubusercontent.com/110176257/187465102-9c42a65e-3d6a-4dc1-b4c0-165e797c910c.png)


### Subnets
A subnet is a range of addresses in your VPC. Subnets reside in single AZs. 

### Gateways 
Gateways allow you to connect your VPC to other networks
#### Internet gateway
an **internet gateway** is a highly available VPC component that allows communication between the VPC and the internet.

### Routing 
Route tables determine where network traffic from your subnet or gateway will be directed.

### CIDR
When you create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a Classless Inter-Domain Routing (CIDR) block. For example, 10.0.0.0/16. This is the primary CIDR block for your VPC.

An IPv4 CIDR block expands upon the IPv4 4 groups of digits by adding a forwards slash at the end - / followed by a number ranging from 0-32. For example; 10.0.0.0/16