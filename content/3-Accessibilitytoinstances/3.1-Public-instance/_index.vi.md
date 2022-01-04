---
title : "Tạo kết nối đến máy chủ EC2 Public"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---
![SSMPublicinstance](/images/3.CreateconnectiontoEC2/SNA1.png)
### Các bước thực hiện sẽ như sau:
- Tạo Linux instance và gán IAM Role chúng ta đã tạo
   ![configinstance](/images/3.CreateconnectiontoEC2/SNA008.png)
- Kiểm tra lại Security group của Linux instance vừa tạo. Đảm bảo rằng outbound cho phép All Traffice tới 0.0.0.0/0 và không cần inbound.
  ![SG](/images/3.CreateconnectiontoEC2/SNA009.png)
- Sau khi tạo xong public instance, bạn vào AWS System Manager -> chọn Session Manager và Start Session.
  ![sessionmanager](/images/3.CreateconnectiontoEC2/SNA010.png)
- Sau đó chọn instance và ấn Start session để truy cập vào instance
  ![startsession](/images/3.CreateconnectiontoEC2/SNA011.png)
- Terminal sẽ xuất hiện trên trình duyệt. Kiểm tra với câu lệnh ``` sudo tcpdump -nn port 22 ``` và ```sudo tcpdump ``` chúng ta sẽ thấy không có traffic của SSH mà chỉ có traffic HTTPS.
   ![testtcpdump](/images/3.CreateconnectiontoEC2/SNA012.png)

{{% notice note %}}
 Ở trên, chúng ta đã tạo  kết nối vào public instance mà không cần mở cổng SSH 22, giúp cho bảo mật tốt hơn, tránh mọi sự tấn công tới cổng SSH.\
Một nhược điểm của cách làm trên là ta phải mở Security Group outbound ở cổng 443 ra ngoài internet. Vì là public instance nên có thể sẽ không vấn đề gì nhưng nếu bạn muốn bảo mật hơn nữa, bạn có thể khoá cổng 443 ra ngoài internet mà vẫn sử dụng được Session Manager. Cách làm này mình sẽ trình bày ở phần private instance dưới đây:
 {{% /notice %}}