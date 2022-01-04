---
title : "Create S3 Bucket to track session logs"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---


{{% notice tip %}}
We will configure S3 (Simple Storage Service) to monitor session logs. 
{{% /notice %}}

### Content:
  - [Attach **AmazonS3FullAccess** policy to IAM Role SSM](#attach-amazons3fullaccess-policy-to-iam-role-ssm)
  - [Create **S3 Bucket**](#create-s3-bucket)
  - [Check **Session logs** in **S3**](#check-session-logs-in-s3)
  

#### Attach **AmazonS3FullAccess** policy to IAM Role SSM

- Back to IAM Role **SSM** console
  ![s3policy](/images/3.CreateconnectiontoEC2/SNA022.png)
- Choose **Attach Policies**
  ![s3policy](/images/3.CreateconnectiontoEC2/SNA023.png)
- Then, type **AmazonS3FullAccess** into the search bar and choose **AmazonS3FullAccess** 
  ![attachpermission](/images/3.CreateconnectiontoEC2/SNA024.png)
- Finally, click **Attach Policy**
  ![ends3policy](/images/3.CreateconnectiontoEC2/SNA025.png)

#### Create **S3 Bucket**
- Go to **S3** console, chooose **Buckets** tab, then select **Create Bucket**
  ![createbucketv0](/images/3.CreateconnectiontoEC2/SNA026.png)
- For **Bucket name**: enter your bucket name.
- For AWS Region: choose **Region** you are handing this lab
- Uncheck **Block all public access** for the sake of lab simplicity. In realistic, please consider security matter.
  ![createbucket](/images/3.CreateconnectiontoEC2/SNA027.png)
- Back to **Session Manager** console, choose **Preferences** tab and click on **Edit**.
  ![editssm](/images/3.CreateconnectiontoEC2/SNA027v1.png)
- For **Send session logs to S3**: click **Enable**
- And choose **S3 bucket** name just created.
  ![S3logging](/images/3.CreateconnectiontoEC2/SNA028.png)

#### Check **Session logs** in **S3**
- We will reconnect **Linux instance** and execute some simple commands. Then return to the **S3** interface to view logs. 
  ![seelog](/images/3.CreateconnectiontoEC2/SNA033.png)
- Click on **file.log** then select **Download** 
  ![seelog1](/images/3.CreateconnectiontoEC2/SNA030.png)
- We wil see **sesion logs** by **Notepad**
  ![openlog1](/images/3.CreateconnectiontoEC2/SNA031.png)