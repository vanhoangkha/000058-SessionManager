---
title : "Port Forwarding"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

{{% notice info %}}
**Port Forwarding** là một cách hữu ích để chuyển lưu lượng từ 1 địa chỉ IP này và 1 port đến 1 địa chỉ IP và 1 port khác. Với **Port Forwarding**, bạn có thể truy cập đến máy ảo EC2 được đặt trong **private subnet** từ máy chủ của bạn.
{{% /notice %}}

Chúng ta sẽ thực hành cấu hình **Port Forwarding** để kết nối RDP giữa máy của chúng ta với **Windows instance** được đặt trong **private instance** được tạo ở [bước 2.2](/accessibilitytoinstances/private-instance/).
![port-fwd](/images/4.Portfwd/SNA033.png) 
- Để thực hành phần này, hãy đảm bảo rằng máy tính của bạn đã cài đặt [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html) và [Seession Manager Plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)
- Chạy câu lệnh dưới đây trên máy tính của bạn để cấu hình **port forwarding**
  ```
  aws ssm start-session --target (your ID windows instance) --document-name AWS-StartPortForwardingSession --parameters portNumber="3389",localPortNumber="9999" --region (your region) 
  ```
 ![runcmd](/images/4.Portfwd/SNA034.png)
- Thực hiện kết nối đến **Windows instance** bằng **Remote Desktop** trên máy của bạn.
  
![rdp](/images/4.Portfwd/SNA035.png) 

- Quay trở lại giao diện **Session manager**, chọn tab **Session history** chúng ta sẽ thấy session log với tên **AWS-StartPortForwardingSession**
 ![checklog](/images/4.Portfwd/SNA032.png) 