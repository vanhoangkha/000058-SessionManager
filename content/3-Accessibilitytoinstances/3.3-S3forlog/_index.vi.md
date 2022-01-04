---
title : "Tạo S3 Bucket để theo dõi session logs"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---


{{% notice tip %}}
Chúng ta sẽ cấu hình S3 ( Simple Storage Service ) để theo dõi session logs.
{{% /notice %}}

### Nội dung:
  - [Gán **AmazonS3FullAccess** policy cho IAM Role SSM](#gán-amazons3fullaccess-policy-cho-iam-role-ssm)
  - [Tạo **S3 Bucket**](#tạo-s3-bucket)
  - [Kiểm tra **Session logs** trong **S3**](#kiểm-tra-session-logs-trong-s3)
  
#### Gán **AmazonS3FullAccess** policy cho IAM Role SSM

- Quay lại giao diện IAM Role **SSM**
  ![s3policy](/images/3.CreateconnectiontoEC2/SNA022.png)
- Chọn **Attach Policies**
  ![s3policy](/images/3.CreateconnectiontoEC2/SNA023.png)
- Sau đó, nhập **AmazonS3FullAccess** vào thanh tìm kiếm và chọn **AmazonS3FullAccess** 
  ![attachpermission](/images/3.CreateconnectiontoEC2/SNA024.png)
- Cuối cùng, nhấn **Attach Policy**
  ![ends3policy](/images/3.CreateconnectiontoEC2/SNA025.png)

#### Tạo **S3 Bucket**
- Truy cập đến giao diện **S3**, chọn tab **Buckets**, sau đó nhấn **Create Bucket**
   ![createbucketv0](/images/3.CreateconnectiontoEC2/SNA026.png)
- Ở phần **Bucket name**: nhập tên bucket.
- Ở phần AWS Region: chọn **Region** bạn đang làm bài thực hành.
 ![createbucket](/images/3.CreateconnectiontoEC2/SNA027.png)
- Bỏ chọn **Block all public access**. Vì đây là bài thực hành đơn giản nên chúng ta có thể bỏ chặn tất cả quyền truy cập công khai. Trong thực tế, vui lòng xem xét lại vấn đề bảo mật.
  ![editssm](/images/3.CreateconnectiontoEC2/SNA027v1.png)
- Trở lại giao diện **Session Manager**, chọn tab **Preferences** và nhấn **Edit**.
   ![S3logging](/images/3.CreateconnectiontoEC2/SNA028.png)
- Ở phần **Send session logs to S3**: chọn **Enable**
- Và chọn tên **S3 bucket** vừa tạo.
  !![seelog](/images/3.CreateconnectiontoEC2/SNA029.png)

#### Kiểm tra **Session logs** trong **S3**
- Chúng ta sẽ kết nối lại **Linux instance** và thao tác 1 số lệnh đơn giản. Sau quay lại giao diện **S3** để xem logs.
  ![seelog](/images/3.CreateconnectiontoEC2/SNA033.png)
- Click vào **file.log** sau đó chọn **Download** 
 ![seelog1](/images/3.CreateconnectiontoEC2/SNA030.png)
- Chúng ta sẽ xem **sesion logs** bằng **Notepad**
  ![openlog1](/images/3.CreateconnectiontoEC2/SNA031.png)