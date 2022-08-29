# Monitoring

Monitoring empowers operators to notice issues before they cause more serious errors, and helps you preserve high availability and deliver high quality of service. It provides you with real-time data and insights to monitor applications, services, and infrastructure in the development environment.

The four golden signals of monitoring are: 
### Latency
- The time it takes to service requests

### Traffic
- The rate of requests, number of connections, and bandwidth consumed to host application

### Errors
- Rate of failed requests


### Saturation
- Expression for how much the service's hosting capacity is taken up by requests. This relies on metrics such as resource utilisation (CPU%, RAM%, DISK%), or network capabilities (such as total bandwidth supported or max connections allowed by cloud provider)


## Cloudwatch

![image](https://user-images.githubusercontent.com/110176257/186434968-83a9709c-953b-4e1d-861a-4b44d7bf349b.png)

Cloudwatch is a monitoring service provided by amazon for their AWS cloud. It collects monitoring and operatinal data from logs, metrics, and events, and visualises it using customisable dashboards so you can get a unified view of your AWS resources, applications, and services.

- Cloudwatch metrics allow developers and operational teams to make more informed choices about the future of the project.
- Allows us to create alarms to be notified when something unexpected happens in the machine, and logs to see exactly what the machine did

### Alert management
In AWS , you are able to create your own alerting policies which describes the circumstances under which you want to be alerted and how you want to be notified. Alerting gives timely awareness to problems in your cloud applications so you can resolve the problems quickly.

Actions to be taken in case of alert are varied dependong on why the alert was raised. It could be to send a notifcation to Amazon Simple Notification Service topic:

![image](https://user-images.githubusercontent.com/110176257/186398844-3ddaf592-0326-4ae4-b59f-0b42dc351428.png)

You can also configure this to send a notification to SMS or Slack.

Another common response to alerts is **automated auto-scaling** which refers to adding more hardware resources to the instance as they are needed.

#### In order to create your own alarm, you must:

- Go to EC2 instances, select the instance you wish to add an alarm to:


- Create cloudwatch alarm

![image](https://user-images.githubusercontent.com/110176257/186629853-4187c591-6eea-4654-94fd-66d8659fc7f4.png)

- Select **ADD notification** in Configure Actions

![image](https://user-images.githubusercontent.com/110176257/186630113-3bdab3cc-84ee-4043-9711-61d485c1477f.png)

- Create new SNS topic and enter your email to be notified.


![image](https://user-images.githubusercontent.com/110176257/186626940-c4742ba4-bf2b-40f2-9bdc-8b3327425090.png)

- Select **monitoring**, then select manage detailed monitoring 
- Select **enable** and confirm
- Select **manage cloudwatch alarms**:

![image](https://user-images.githubusercontent.com/110176257/186627306-308c01f1-8ab1-4a52-baab-b17157c1e32b.png)

- Select the SNS topic you created:

![image](https://user-images.githubusercontent.com/110176257/186627522-1daa9319-da83-4361-b7d5-bd2de8c0046a.png)

- Configure your alarm:

![image](https://user-images.githubusercontent.com/110176257/186627718-0d99cc66-2cf0-4fb8-9f41-fccd1b74e7bc.png)


### Logs

[Follow this documentation to set up the CloudWatch Logs agent on a running EC2 Linux instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html)

- Installed log agent with `curl https://s3.amazonaws.com//aws-cloudwatch/downloads/latest/awslogs-agent-setup.py -O`
- Configured log agent with `sudo python ./awslogs-agent-setup.py --region eu-west-1`  Running this command creates a log group and log stream with your selected information.

![image](https://user-images.githubusercontent.com/110176257/186506743-175b5f74-6efe-4c19-9159-50e96c24ce31.png)

Log group created:

![image](https://user-images.githubusercontent.com/110176257/186507419-532a3f1d-4ecc-4574-9546-18064dde1506.png)

Log streams created:

![image](https://user-images.githubusercontent.com/110176257/186507494-e4383ae7-13d8-4b7c-a449-320184d6b510.png)

Events are logged:

![image](https://user-images.githubusercontent.com/110176257/186507570-e985d418-59f3-4ee0-b1a3-c274161b50cc.png)

#### Exporting logs to a S3 bucket

You must edit the bucket permissions first, you can do this by [following the official documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3ExportTasksConsole.html)

I have simply used the example policy as seen on the documentation:

- In the Amazon S3 console, choose your bucket
- Choose **Permissions**, **Bucket policy**
- In the **Bucket Policy Editor**, I've added the example policy from the official documentation linked above:

![image](https://user-images.githubusercontent.com/110176257/186508744-1318393a-2530-4d63-bef5-533137e5e083.png)


Now you can export your logs to the S3 bucket.

- Open the CloudWatch console
- Choose **Log groups.**
- Choose **Actions**, **Export data to Amazon S3.**

![image](https://user-images.githubusercontent.com/110176257/186509916-84986b6d-6a8b-4be8-833e-5d8cbe68ab0a.png)

- Define the from and to time of logs to be exported
- Select bucket
- Choose **Export**

![image](https://user-images.githubusercontent.com/110176257/186510138-cd97f9c8-6606-4861-8cc6-e8112f2dccdf.png)

Log files are in bucket:

![image](https://user-images.githubusercontent.com/110176257/186510465-72a24b77-01e6-4e6a-b6b3-ae7b0d42c752.png)


### Amazon SNS
Amazon Simple Notification Service (SNS) is a cloud-based web service that delivers messages. All messages published to Amazon SNS are stored across several availability zones to prevent loss.

![image](https://user-images.githubusercontent.com/110176257/186498273-e8bd350e-fc95-4ba3-abc3-8aa42dcec460.png)


### Amazon SQS 
Amazon Simple Queue Service (SQS) is a managed message queuing service deveopers and operations teams use to manage high numbers of alerts from SNS




