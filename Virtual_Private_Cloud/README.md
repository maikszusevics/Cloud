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

# Creating a VPC in AWS

![image](https://user-images.githubusercontent.com/110176257/187691095-398ed845-529f-48f2-be0a-dccfe42f4497.png)

### **step 1: Create VPC with CIDR block 10.0.0.0/16**

![image](https://user-images.githubusercontent.com/110176257/187691369-5043e122-2cd2-4885-b1dd-99287e7cf6ac.png)

- Select **VPC only**
- Add name
- Input CIDR
- Add Name tag

### **step 2: Create internet gateway and add it to VPC**
![image](https://user-images.githubusercontent.com/110176257/187691783-9a21c437-d412-4c61-a718-a256e20fa248.png)

- Attatch to VPC by selecting gateway and selecting attatch option in **actions**

### **step 3: create a public subnet (10.0.5.0/24)**

- Select **subnets** from left column in VPC dashboard
- Select **create subnet** on top right 
- Name subnet, select no preference for AZ, add personal CIDR block, add name tag

### **step 4: Create route table and edit rules**

- edit to allow internet gateway
- Change main route table to your created route table 

![image](https://user-images.githubusercontent.com/110176257/187729685-10c154a6-546a-4bd0-9adc-5183636a80d4.png)


## Deploying app with all pages working
### Create private subnet
- Go to VPC dashboard
- Select "subnets"
- Select "create subnet"
- Select your VPC
- Make up an unused CIDR block 
- add name tag 

- Create route table for private subnet, **DO NOT ADD INTERNET GATEWAY TO PRIVATE SUBNET**

![image](https://user-images.githubusercontent.com/110176257/187729452-94a85c5c-191e-4caf-8b53-05681d24c822.png)


### Launch DB AMI on *private* subnet:
*note: do not need to ssh into db*


### Launch App AMI on public subnet
*note: my AMI runs app on launch:*
![image](https://user-images.githubusercontent.com/110176257/187729915-f65ca4d4-8e20-4d75-b241-75a2e6b49e75.png)
- SSH into app machine 
- Edit `.bashrc` file to change `DB_HOST` variable with new **private** IP address of DB machine
- run `source .bashrc` to enable the change 
- run `node seed.js` in `app/seeds/`
- run `npm start`

![image](https://user-images.githubusercontent.com/110176257/187732729-e3d03de2-2874-4396-b65b-99fd5f3e7828.png)





