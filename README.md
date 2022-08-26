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

## Benefits of cloud computing
- Don't have to buy bespoke hardware for large projects (cost effective)
- Go global in minutes
- Scalable


# Sparta guidelines for AWS usage

- AWS naming convention for services - group_person_task - for example - eng122_Shahrukh_ec2

- When not in use (09:00 - 18:00) terminate. It costs money to run. Ask if you want to run out of hours, so that it can be authorised.

- for the duration of this course ensure you are logged in in Ireland - Europe (Ireland) eu-west-1.

- Do not delete anyone else's services

- DO NOT share AWS account details or keys with anyone - so don't push them to github


# Disaster Recovery

Disasters can happen for any reason and are not predictable. If you do not have a disaster recovery plan, it could permanently wipe out your data.

You can lower tha chances of this by:
- Having your own local backups (Hybrid Cloud)
- Having your data stored on multiple AZs, for example eu-west-1a, and eu-west-1b and 1c. If one of these datacentres goes down, your data will still be safe in the other locations.
- Having data stored accross multiple regions
- Deploying your data across multiple cloud service providers. This is very expensive but It's neccesary for situations where very sensitive data is being stored, such as government records or bank details.

![disaster](https://user-images.githubusercontent.com/110176257/186161523-0b7efed5-cabc-4db7-962d-620c1b16e644.png)


![image](https://user-images.githubusercontent.com/110176257/186168870-44b62756-7f87-4d5d-afba-f980928b1ebb.png)

## Amazon S3

