
# **IAM basics**
IAM stands for **identity and access management**, IAM is not a region specific service, it is global and users/groups are created accross all regions.

IAM users, groups, and policies are initially set up by the AWS **root user**


## IAM groups and users

The first user that is created when you make an AWS account is the **root user**.
The root user has all the permissions, making it the most powerful user. However, especially in large organisations, the most powerful user is also the most dangerous user as you can accidentally cause irreprable damage to the cloud infrastructure or data storage. 

In best practise, the ***root user*** is only used to create the accounts and IAM infrastructure, and ideally nothing else. Administrative roles are not done by the root user, instead you use root user to create **admin users**, and then specify the permissions that they need to perform administrative duties.

[instructions for creating an admin user](https://github.com/maikszusevics/Cloud/blob/main/IAM/Creating_IAM_user/README.md)


- Groups cannot contain other groups
- Users dont have to belong to a group 
- Users can belong to multiple groups

![image](https://user-images.githubusercontent.com/110176257/193119594-a268646a-70d6-4a47-85f6-2075910b5370.png)


## IAM policies
An IAM policy defines the permissions of a group, role, or user. 
Most policies are inherited from groups, a policy is assigned at the group level and all users assigned to this group inherit the permissions set by the policy. A policy can also be made for a user that's not in a group, these are called **inline** policies. 
- Users that are members of multiple groups inhrerit policies from all groups they are in
- Policies are defined in JSON documents

### IAM JSON structure
Here is an example JSON file that defines an IAM policy:

![image](https://user-images.githubusercontent.com/110176257/193251215-40cb311b-910d-4557-8bf7-c9080ebbb690.png)


- Version: policy language version, always include "2012-10-17"
- Id: Identifier for the policy (optional)
- Statement: one or more individual statements 
  - Sid: an identifier for the statement (optional)
  - Effect: whether the statement allows or denies access to certain APIs 
  - Principal: account/user/role to which the policy is applied to 
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions apply to 
  - Condition: conditions for when this policy is in effect (optional)
  
  
