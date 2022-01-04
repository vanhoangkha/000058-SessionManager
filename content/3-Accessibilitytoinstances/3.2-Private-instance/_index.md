---
title : "Create connection to EC2 Private instance "
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---

For **Windows instance** located in **private subnet**, there is no **public IP**, no **internet gateway** so cannot go out **internet.**\
With this type of instance, the traditional way is to use Bastion host technique which takes a lot of money and effort, but here we will use Session Manager with this type.\
Basically, the **private instance** still has to open the **TCP 443** port to **System Manager**, but don't let that connection go out to the internet, but only in its own VPC, so make sure be security problem.\
To do that, we must include the System Manager endpoint in the VPC, that is, using the **VPC interface endpoint.** 
![SSMPrivateinstance](/images/3.CreateconnectiontoEC2/SNA0.png)
**VPC interface endpoint** is attached to the subnet, so this method can be done not only with **private subnet** but also with **public subnet**, which means that with **public subnet**, you completely can not let **TCP 443** go out to the internet.

### Content:
  - [Create VPC Endpoint](#create-vpc-endpoint)
  - [Create Private Instance](#create-private-instance)

### Create VPC Endpoint

- We will create 4 interface endpoints and 1 gateway endpoint: 
  - Interface endpoint:
    - com.amazonaws.region.ssm
    - com.amazonaws.region.ec2messages
    - com.amazonaws.region.ec2
    - com.amazonaws.region.ssmmessages
  - Gateway endpoint:
     - com.amazonaws.region.s3
- Access to **VPC** console, choose **Endpoint**, then select **Create Endpoint** 
  ![endpointtheme](/images/3.CreateconnectiontoEC2/SNA013.png)
- For **Service catelogy** choose:  **AWS services**
- For **Service Name** choose: **SSM**
  ![createenpoint](/images/3.CreateconnectiontoEC2/SNA014.png)
- For **Subnet**, choose subnet containing **Windows instance**
- Check **Enable DNS name** 
  ![createenpoint](/images/3.CreateconnectiontoEC2/SNA014.1.png)
- For **Security Group**, choose the Security group of the private subnet we created.
- For **Policy**, chọn **Full access**
  ![createendpointv1](/images/3.CreateconnectiontoEC2/SNA015.png)
- We have created VPC Interface Endpoint for **SSM**, we need to create 3 more VPC Interface Endpoints for **ssmmessages**, **ec2**, **ec2messages** and VPC Gateway Endpoint services for **SSM**. **S3** with the same method as above.
  ![createendpointv2](/images/3.CreateconnectiontoEC2/SNA016.png)

### Create Private Instance
- We will create a **Windows instance** located in **private subnet** with connection to **VPC Endpoint** just created above, without **public IP**, choose **IAM Role* * created for the **SSM** service.
   ![ec2-window](/images/3.CreateconnectiontoEC2/SNA017.png) 

- Check the Security group of the Windows instance. Ensure that outbound allows All Traffice tới 172.31.0.0/16 and no need to inbound.
  ![ec2-window](/images/3.CreateconnectiontoEC2/SNA018.png) 
- When created the Windows instance, go back to **System Manager** console, choose the **Session Manager** or **Fleet Manager** tab and see the private instance appears as successful. 
   ![checkwindowsinstance](/images/3.CreateconnectiontoEC2/SNA019.png)
- We will try connecting to **Windows instance** by **Fleet Manager** 
   ![testconnectprivateec2](/images/3.CreateconnectiontoEC2/SNA020.png) 

   ![testconnectprivateec2](/images/3.CreateconnectiontoEC2/SNA021.png) 