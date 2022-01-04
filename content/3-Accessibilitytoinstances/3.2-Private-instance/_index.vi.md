---
title : "Tạo kết nối đến máy chủ EC2 Private"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---
Đối với **Windows instance** nằm trong **private subnet**, không có **public IP**, không có **internet gateway** nên không thể đi ra ngoài **internet.**\
Với loại instance này, cách làm truyền thống là ta sẽ sử dụng kỹ thuật Bastion host tốn nhiều chi phí và công sức, nhưng ở đây chúng ta sẽ sử dụng Session Manager với loại này.\
Cơ bản là **private instance** vẫn phải mở cổng **TCP 443** tới **System Manager**, nhưng không cho kết nối đó đi ra ngoài internet mà chỉ cho đi trong chính VPC của mình, nên đảm bảo được vấn đề bảo mật.\
Để làm được điều đó, ta phải đưa endpoint của System Manager vào trong VPC, nghĩa là sử dụng **VPC interface endpoint:** 
![SSMPrivateinstance](/images/3.CreateconnectiontoEC2/SNA0.png)
**VPC interface endpoint** được gắn với subnet nên cách làm này không những với **private subnet** mà còn có thể làm với **public subnet**, nghĩa là với **public subnet**, bạn hoàn toàn có thể không cho **TCP 443** đi ra ngoài internet.

### Nội dung:
   - [Tạo VPC Endpoint](#tạo-vpc-Endpoint)
   - [Tạo Private Instance](#tạo-Private-Instance)

### Tạo VPC Endpoint

- Chúng ta sẽ tạo 4 interface endpoint và 1 gateway endpoint:\
  - Interface endpoint:
    - com.amazonaws.region.ssm
    - com.amazonaws.region.ec2messages
    - com.amazonaws.region.ec2
    - com.amazonaws.region.ssmmessages
  - Gateway endpoint:
     - com.amazonaws.region.s3
- Truy cập đến giao diện **VPC** chọn **Endpoint**, sau đó chọn **Create Endpoint**
   ![endpointtheme](/images/3.CreateconnectiontoEC2/SNA013.png)
- Ở phần **Service catelogy** chọn:  **AWS services**
- Ở phần **Service Name** nhập: **SSM**
  ![createenpoint](/images/3.CreateconnectiontoEC2/SNA014.png)
- Ở phần **Subnet**, chọn subnet chứa **Windows instance**
- Check **Enable DNS name**
  ![createenpoint](/images/3.CreateconnectiontoEC2/SNA014.png)
- Ở phần **Security Group**, chọn Security group của private subnet mà chúng ta đã tạo trước đó.
- Ở phần **Policy**, chọn **Full access**
   ![createendpointv1](/images/3.CreateconnectiontoEC2/SNA015.png)
- Chúng ta đã tạo xong VPC Interface Endpoint cho **SSM**, chúng ta cần tạo thêm 3 VPC Interface Endpoint cho các dịch vụ **ssmmessages**, **ec2**, **ec2messages** và VPC Gateway Endpoint cho **S3** với cách làm tương tự như trên.
    ![createendpointv2](/images/3.CreateconnectiontoEC2/SNA016.png)

### Tạo private instance
- Chúng ta sẽ tạo 1 **Windows instance** nằm trong **private subnet** có kết nối tới **VPC Endpoint** vừa tạo ở trên, không có **IP public**, chọn **IAM Role** đã tạo cho dịch vụ **SSM** ở phần đầu.
   ![ec2-window](/images/3.CreateconnectiontoEC2/SNA017.png)  
- Kiểm tra lại Security group của Linux instance vừa tạo. Đảm bảo rằng outbound cho phép All Traffice tới 172.31.0.0/16 và không cần inbound.
 ![ec2-window](/images/3.CreateconnectiontoEC2/SNA018.png)  
- Sau khi tạo xong Windows instance, trở lại **System Manager**, chọn tab **Session Manager** hoặc **Fleet Manager** và thấy private instance xuất hiện là đã thành công.
   ![checkwindowsinstance](/images/3.CreateconnectiontoEC2/SNA019.png)
- Chúng ta sẽ thử kết nối đến **Windows instance** thông qua **SSM** 
  ![testconnectprivateec2](/images/3.CreateconnectiontoEC2/SNA020.png) 
   ![testconnectprivateec2](/images/3.CreateconnectiontoEC2/SNA021.png) 