# Cloud

![image](https://user-images.githubusercontent.com/110176257/185875226-ecc9aa30-921e-477b-a048-98538d965282.png)


## What is cloud computing

![image](https://user-images.githubusercontent.com/110176257/185875183-78cae1b5-d9c2-4206-954e-db57503285ea.png)


## AWS Global infrastructure


![image](https://user-images.githubusercontent.com/110176257/185875309-fc36dfa4-7c14-4b9e-8a2d-b8c39b73f80d.png)

## SAAS (software as a service)

![image](https://user-images.githubusercontent.com/110176257/185875520-400cfd81-1be2-49e8-8e56-2da62df1fb4a.png)



Some of the drawbacks of SAAS include:

- Lack of customisation
- Dont own the platform
- Less control over hosting


### PAAS (platform as a service)


![image](https://user-images.githubusercontent.com/110176257/185875808-6a7d249a-1492-485b-856c-7b87a8e9d3af.png)


- When we are creating VM's on amazon AWS, we are using AWS Platform As A Service.

### IAAS (infrastructure as a service)
Infrastructure as a cloud service aims to provide all of the building blocks of an IT system, including machines, globally available applications/services, and data storage.

![image](https://user-images.githubusercontent.com/110176257/185876327-16d93435-f175-4c7d-9d77-7085a9615a62.png)




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



# Provisioning an EC2 instance at `user details`

First we will launch an instance like we did earlier in the document:

- Select the same Ubuntu 18.04 AMI

![image](https://user-images.githubusercontent.com/110176257/185911520-c8d8fa1b-3c9b-4340-a0e7-a4832548e46a.png)

- Default T2 hardware settings as this will only be an example

### Add provisioning script at the bottom of Configure Instance Details section User Details

![image](https://user-images.githubusercontent.com/110176257/185922969-b9aae500-5a25-4b59-8ead-53a89bf9318c.png)



# AMIs (Amazon Machine Images)

A machine image is an operating system, including all of the data that was on this system at the time the image was created. Any software installed, configurations made, data stored, will all be on the image as well.

AMIs in this example:

![clout](https://user-images.githubusercontent.com/110176257/185962075-0038436d-bb9e-42e0-be79-40df24823442.png)

The image shows how the EC2 instances are created using an AMI, and then an AMI is created out of the instance we created and modified.

In order to create a new AMI from an existing instance, you must go to the ec2 dashboard, then instances, and then select the isntance you wish to image.

Once selected, open the `actions` ribbon and select `image and templates`

![image](https://user-images.githubusercontent.com/110176257/185963825-a2c5d770-7e2c-4896-adb2-e6ae1e3d59cd.png)

and from here click `create image`

- Give it a name and description

![image](https://user-images.githubusercontent.com/110176257/185964249-41a46555-5891-40b3-875e-2c8d36fa4fd7.png)

- REMEMBER to follow proper naming conventions, it is important 
- Create image

![image](https://user-images.githubusercontent.com/110176257/185964367-f578927c-dabf-4634-b0ff-ad83e43ccf2c.png)






