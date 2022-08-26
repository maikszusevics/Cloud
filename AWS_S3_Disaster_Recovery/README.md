# Disaster Recovery

Disasters can happen for any reason and are not predictable. If you do not have a disaster recovery plan, it could permanently wipe out your data.

You can lower tha chances of this by:
- Having your own local backups (Hybrid Cloud)
- Having your data stored on multiple AZs, for example eu-west-1a, and eu-west-1b and 1c. If one of these datacentres goes down, your data will still be safe in the other locations.
- Having data stored accross multiple regions
- Deploying your data across multiple cloud service providers. This is very expensive but It's neccesary for situations where very sensitive data is being stored, such as government records or bank details.

![disaster](https://user-images.githubusercontent.com/110176257/186161523-0b7efed5-cabc-4db7-962d-620c1b16e644.png)


# Amazon S3

S3 is Amazon Simple Storage service.

It is  globally available storage, it is not AZ specific. So if one AZ goes down, your data is not lost and still accessible. This makes it suitable for backup and recovery storage.

## AWSCLI
Amazon have their own command line interface that is written in python. We can use this to control AWS services from our terminal. It also allows us to create python scripts which automate tasks.

The prerequisites of scripting S3 tasks are:
- AWSCLI installed
- Python 3.7 or above install
- PIP3 installed
- AWS config with access and secret keys
- boto3

### Creating an S3 bucket:
```python
import boto3

# creates function for making bucket
def makebucket():

        # asks for location and name

        location = input("where will this bucket be stored? ")
        name = input("Name your bucket: ")
        s3 = boto3.client('s3', region_name=location)

        # interacts with s3 api with input info to make bucket

        s3.create_bucket(Bucket=name, CreateBucketConfiguration={'LocationConstraint':location})

# calls function
makebucket()

```

### Uploading to S3 bucket:
```python
# import boto 3 module
import boto3

# create function to upload files

def uploader():
        filename = input("file name/directory? ")
        bucket  = input("name of the bucket? ")
        s3 = boto3.client('s3')
        s3.upload_file(filename, bucket, filename)

uploader()
```
### Deleting from S3 bucket
```python
import boto3

s3 = boto3.client('s3')

s3.delete_object(Bucket='eng122-maiks-botobucket', Key='test.txt')
```
### Deleting bucket:
```python 
import boto3

s3 = boto3.client('s3')

s3.delete_bucket(Bucket='eng122-maiks-botobucket')
```