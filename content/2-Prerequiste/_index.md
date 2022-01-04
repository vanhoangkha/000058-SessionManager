---
title : "Prerequistes"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
You need to create 1 Linux instance on the public subnet and 1 Windows instance on the private subnet to perform this lab. 
{{% /notice %}}

To use System Manager to manage our window instance in particular and our instances in general on AWS, we need to give System Manager permission to access your instance. 
### Content
   - [Create IAM Role](#create-iam-role)
   - [Create security group for public subnet](#create-security-group-for-public-subnet)
   - [Create security group for private subnet](#create-security-group-for-private-subnet)
   - [Create security group for VPC Endpoint](#create-security-group-for-vpc-endpoint)

### Create IAM Role
2.1. Sign in to the **AWS Console** at https://aws.amazon.com/console/\
2.2. Navigate to the **IAM** console.\
2.3. In the left navigation pane, select **Roles.** 

![role](/images/2.prerequistes/SNA000.png)

2.4. Choose **Create role**.\
2.5. Choose **AWS service** and select **EC2**. Then select **Next: Permissions**

![role1](/images/2.prerequistes/SNA001.png)

2.6. Find ***AmazonSSMManagedInstanceCore*** and select it. Then select **Next: Tags.**
![createpolicy](/images/2.prerequistes/SNA003.png)
2.7. **(Optional)** You can add tags to the role.\
2.8. Click **Next: Review.**\
2.9. Name the Role at Role Name. Then select **Create Role**.
![namerole](/images/2.prerequistes/SNA004.png)

### Create security group for public subnet
- Create a security group for the public instance:
   - No need to inbound
   - Outbound : allow All Traffic to 0.0.0.0/0 

![SG-public](/images/2.prerequistes/SNA005.png) 

### Create security group for private subnet
- Create a security group for the private instance:
   - No need to inbound
   - Outbound : allow TCP 443 to 172.31.0.0/16 (my VPC CIDR) 
   
![SG-private](/images/2.prerequistes/SNA006.png)

### Create security group for VPC Endpoint
- Create security group for VPC Endpoint:
   - Inbound: allow TCP 443 to 172.31.0.0/16 (my VPC CIDR)
   - No need to outbound 
  
![SG-private](/images/2.prerequistes/SNA007.png)
   
