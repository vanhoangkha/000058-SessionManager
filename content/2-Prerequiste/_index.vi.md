---
title : "Các bước chuẩn bị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Bạn cần tạo sẵn 1 Linux instance thuộc public subnet và 1 Window instance thuộc private subnet để thực hiện bài thực hành này.
{{% /notice %}}

Để sử dụng System Manager để quản lý window instance nói riêng và các instance nói chung của chúng ta trên AWS, ta cần phải cung cấp quyền cho System Manager truy cập vào instance của chúng ta.
### Nội dung
  - [Tạo IAM Role](#tạo-iam-role)
  - [Tạo security group cho public subnet](#tạo-security-group-cho-public-subnet)
  - [Tạo security group cho private subnet](#tạo-security-group-cho-private-subnet)
  - [Tạo security group cho VPC Endpoint](#tạo-security-group-cho-vpc-endpoint)
  
### Tạo IAM Role
2.1. Đăng nhập vào AWS Console tại https://aws.amazon.com/console/ \
2.2. Điều hướng đến IAM console.\
2.3. Ở thanh điều hướng bên trái chọn Roles.
![role](/images/2.prerequistes/SNA000.png)
2.4. Chọn Create role.\
2.5. Chọn AWS service và chọn EC2. Sau đó chọn Next: Permissions 
![role1](/images/2.prerequistes/SNA001.png)
2.6. Tìm AmazonSSMManagedInstanceCore và chọn nó. Sau đó chọn Next: Tags.
![createpolicy](/images/2.prerequistes/SNA003.png)
2.7. (Optional) Bạn có thể thêm tag cho role.\
2.8. Nhấn chọn Next: Review.\
2.9. Đặt tên cho Role ở Role Name. Sau đó chọn Create Role.
![namerole](/images/2.prerequistes/SNA004.png)

### Tạo security group cho public subnet 
- Chúng ta sẽ tạo security group cho public instance:
  - Không cần inbound 
  - Outbound : cho phép All Traffic tới 0.0.0.0/0
  ![SG-public](/images/2.prerequistes/SNA005.png) 

### Tạo security group cho private subnet 
- Chúng ta sẽ tạo security group cho private instance:
  - Không cần inbound 
  - Outbound : cho phép TCP 443 tới 172.31.0.0/16 (CIDR VPC của mình)
   
![SG-private](/images/2.prerequistes/SNA006.png)

### Tạo security group cho VPC Endpoint
- Chúng ta sẽ tạo security group cho VPC Endpoint:
  - Inbound: cho phép TCP 443 tới 172.31.0.0/16 (CIDR VPC của mình)
  - Không cần outbound
    
![SG-private](/images/2.prerequistes/SNA007.png)
