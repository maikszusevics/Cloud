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


Now you can move to the AMIs section.

![image](https://user-images.githubusercontent.com/110176257/186107150-8e82579e-7d4f-4554-a1ea-dda8354080dd.png)

From this menu, you can find your new image by searching your name in the bar, if you followed the proper naming convention.

From that stage you can set up the instance in the same way we did before. Make sure you read the details you have given yourself about the images.

When you SSH into your new machine made from your AMI, you may have to change "root" in the ssh command to "ubuntu" otherwise it wont let you connect.

![image](https://user-images.githubusercontent.com/110176257/186110769-712e1563-4273-4169-a75c-cc4b85371a66.png)

By running the command `printenv` in our app machine, we can see that the DB_HOST variable is using the outdated db IP,
![image](https://user-images.githubusercontent.com/110176257/186111058-4e7d95be-9bd0-4243-a9a0-244228ba4208.png)

we can rectify this by using the command `sudo nano .bashrc` and editing the IP address from there.

Make sure you type `source .bashrc` after editing this file.

Make sure that the private IP adress of the APP machine:

![image](https://user-images.githubusercontent.com/110176257/186112739-1a7915f9-21fb-4f16-8f21-9a8b0693a6cc.png)


Is in the security group for port 27017 in the DB machine. This means the DB will allow only the app machine to fetch mongodb data.

![image](https://user-images.githubusercontent.com/110176257/186113039-bae9c639-a3bc-49ad-a076-3ca924c390ca.png)


Make sure that mongodb is running using `sudo systemctl status mongod`:

![image](https://user-images.githubusercontent.com/110176257/186113211-76e6dcaf-422f-4541-9162-a52953e16d70.png)


Now on APP machine, navigate to app/seeds/ and use command `sudo node seed.js`

![image](https://user-images.githubusercontent.com/110176257/186114189-7d9418cd-dc1c-45f2-941d-14c871e3a9e4.png)

If you see the message "database cleared, database seeded" it has worked, and you can go back to app by `cd ..` and then `npm start`.

If you've followed all the steps, you should be able to see the posts page as well as the default.

![image](https://user-images.githubusercontent.com/110176257/186115117-38063cc0-3f22-4507-b298-a1eca4ed941d.png)
