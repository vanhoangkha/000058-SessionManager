---
title : "Port Forwarding"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

{{% notice info %}}
**Port Forwarding** is a useful way to redirect network traffic from one IP address and port number combination to another. With **port forwarding**, you can access an **EC2 instance** located in a **private subnet** from your workstation.
{{% /notice %}}

We will configure **Port Forwarding** for RDP connection between our machine with **Windows instance** placed in **private instance** created in [step 2.2](/accessibilitytoinstances/private-instance/).  
 ![port-fwd](/images/4.Portfwd/SNA033.png) 
- To do this part, ensure your computer has been installed [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html) and [Seession Manager Plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)
- Run the command below on your computer to configure **port forwarding**
  ```
  aws ssm start-session --target (your ID windows instance) --document-name AWS-StartPortForwardingSession --parameters portNumber="3389",localPortNumber="9999" --region (your region) 
  ```
 ![runcmd](/images/4.Portfwd/SNA034.png)
- Connect to **Windows instance** by **Remote Desktop** on your machine.
  
 ![rdp](/images/4.Portfwd/SNA035.png) 

- Back to **Session manager** console, select **Session history** tab, we will see session logs with document name **AWS-StartPortForwardingSession**
 ![checklog](/images/4.Portfwd/SNA032.png) 