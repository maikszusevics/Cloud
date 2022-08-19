# Cloud

## AWS Global infrastructure


![image](https://user-images.githubusercontent.com/110176257/185669702-2bd82026-a73e-4712-88ef-9c726f9f5cf2.png)

The AWS hardware is interconnected using a highly available, low latency private network infrastructure with fully redundant 100GbE trans-oceanic fibre cables. It provides services in over 240 Countries and Territories. The global infrastructure leads in availability, flexibility, and performance. It also has many security features.

### SAAS (software as a service)
SAAS refers to the cloud provider hosting applications and making them available to end users globally.

Some of the main benefits of SAAS are:

Cost efficient
No hardware costs
Pay only for what you use
Easy implementation
Less operational hassle
No hardware installation
Quicker updates
Access to richer functionality such as analytics
Some of the drawbacks of SAAS include:

Lack of customisation
Dont own the platform
Less control over hosting
### PAAS (platform as a service)
PAAS refers to having a complete development and/or deployment environment hosted on the cloud.

Some of the main benefits of PAAS are:

Rapid delivery of new capabilities
Scalable
Flexible
Faster time to market
Economical cost of tools
Less operations required
When we are creating VM's on amazon AWS, we are using AWS Platform As A Service.

### IAAS (infrastructure as a service)
Infrastructure as a cloud service aims to provide all of the building blocks of an IT system, including machines, globally available applications/services, and data storage.

No maintainance resposibilities
On-demand access
Constant monitoring
Less downtime
Improved security
Enterprise grade infrastructure
Pay per use



# Two-tier architechture app deployment


![image](https://user-images.githubusercontent.com/110176257/185664004-ebf7e157-af9a-4c3c-b5a8-21a73a5f0945.png)


## Benefits of cloud computing
- Don't have to buy bespoke hardware for large projects (cost effective)
- Go global in minutes
- Scalable

## Steps for creating a new VM instance on Amazon AWS

- From the home console, click 

![image](https://user-images.githubusercontent.com/110176257/185451890-4e30245e-e6c5-4e97-ba64-88fda0d3c6c1.png)


- From the home console, click on EC2
- Once in EC2 dashboard, click launch instance without template

![image](https://user-images.githubusercontent.com/110176257/185461927-ea2abfae-ebcc-4fb9-9ed3-8cfa487c55f4.png)


- Scroll on OS select until you reach `Ubuntu Server 18.04 LTS (HVM), SSD Volume Type`, use this one as it is the one we tested the app with.

- Select T2 micro default instance type

![image](https://user-images.githubusercontent.com/110176257/185574359-2de8b33a-70c0-4679-9711-eb8c470e67d3.png)

- Use 1a subnet setting with auto assign ip enabled

![image](https://user-images.githubusercontent.com/110176257/185574393-2123e7b4-4dfc-4148-85e0-16efefbb59b1.png)

- Use default storage configuration 

- Add a name tag

![image](https://user-images.githubusercontent.com/110176257/185574735-2dfbc86c-81d3-4416-a382-5f5c2b33529a.png)

I am using these network settings:

![image](https://user-images.githubusercontent.com/110176257/185574921-3c9c1b5a-d321-483b-b9f2-c1b636ad9035.png)


### Select your instance from the instanced menu and click "connect"

- Next navigate to the SSH client and copy the bottom command

![image](https://user-images.githubusercontent.com/110176257/185575781-17fd84af-787c-46c0-85b4-36337ce5017b.png)

- Enter this command into the terminal at your .ssh folder in order to connect to the machine.

#### Installing dependencies within the VM

To install all the dependencies, i've run the following commands:
```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install nginx -y
sudo systemctl enable ngninx 
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - 
sudo apt-get install -y nodejs
# I have reverse proxy config saved, it uses this command: proxy_pass http://localhost:3000;
sudo cp -f all_app/app/reverse_proxy /etc/nginx/sites-available/default 
sudo systemctl restart nginx
cd all_app
cd app
sudo apt-get install npm
npm install express -y
npm install mongoose -y
npm install
npm start
```








![image](https://user-images.githubusercontent.com/110176257/185454174-bf841931-427c-48a9-a952-efc6a801dd6e.png)


![image](https://user-images.githubusercontent.com/110176257/185581581-6833113c-999a-477c-ba9a-ba3d92471443.png)



# Sparta guidelines for AWS usage

- AWS naming convention for services - group_person_task - for example - eng122_Shahrukh_ec2

- When not in use (09:00 - 18:00) terminate. It costs money to run. Ask if you want to run out of hours, so that it can be authorised.

- for the duration of this course ensure you are logged in in Ireland - Europe (Ireland) eu-west-1.

- Do not delete anyone else's services

- DO NOT share AWS account details or keys with anyone - so don't push them to github




## Setting up DB machine 

Use previous guide, this time include TCP port 27017 for your app to connect.

Once inside the DB VM, run these commands to install dependencies:
```
sudo apt-get update
sudo apt-get upgrade -y
        
# retrieves key from mongodb
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927
echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
        
# updates ubuntu
sudo apt-get update
sudo apt-get upgrade -y
        
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

sudo Nano /etc/mongod.conf # Edit the IP in this to be your app machine's IP

# enables and starts mongodb
sudo systemctl restart mongod
sudo systemctl enable mongod
```

##### Now back inside APP machine

Create environment varaible for DB_HOST by running:
```
export DB_HOST=mongodb://DBMACHINEIP/posts
```
Navigate to `app/seeds`, run command `sudo node seed.js`, then `cd ..`, and `npm start` again.

![image](https://user-images.githubusercontent.com/110176257/185666440-a9187028-b175-4be3-92ca-fad2805c8fa0.png)
