---
title : "Create connection to EC2 Public instance"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

  ![SSMPublicinstance](/images/3.CreateconnectiontoEC2/SNA1.png)
### The steps will be as follows: 
- Create the Linux instance and attach the IAM Role SSM to it.
  
  ![configinstance](/images/3.CreateconnectiontoEC2/SNA008.png)

- Check the Security group of the Linux instance. Ensure that outbound allows All Traffice tới 0.0.0.0/0 and no need to inbound.
 
  ![SG](/images/3.CreateconnectiontoEC2/SNA009.png)
  
- After creating the public instance, go to AWS System Manager -> select Session Manager and Start Session. 
 
  ![sessionmanager](/images/3.CreateconnectiontoEC2/SNA010.png)

- Then select the instance and click Start session to access the instance 

  ![startsession](/images/3.CreateconnectiontoEC2/SNA011.png)

- Terminal will appear in the browser. Test with the command  ``` sudo tcpdump -nn port 22 ``` và ```sudo tcpdump ```we will see the result no SSH traffic but outboud HTTPS. 

  ![testtcpdump](/images/3.CreateconnectiontoEC2/SNA012.png)

 
{{% notice note %}}
 Above, we have created a connection to the public instance without opening SSH port 22, for better security, avoiding any attack to the SSH port.\
 One drawback of the above method is that we have to open the Security Group outbound at port 443 to the internet. Since it's a public instance, it probably won't be a problem, but if you want even more security, you can block port 443 to the internet and still use the Session Manager. How to do this I will demonstrate in the private instance section below. 
{{% /notice %}}
