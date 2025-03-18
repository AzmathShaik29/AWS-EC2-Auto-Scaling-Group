1. Create VPC

![image](https://github.com/user-attachments/assets/8d5d09b1-df11-4512-89dc-a42bf28e32c4)

2. Create IGW

![image](https://github.com/user-attachments/assets/72060f66-bc0f-47f2-9f27-258b451f3c30)

3. Attach the IGW to VPC which created in Step 1

![image](https://github.com/user-attachments/assets/f5ed4920-9272-4a79-be86-cc9b2c546657)

4. Create 2 subnets

![image](https://github.com/user-attachments/assets/fc9c00af-0030-4b7e-ad25-16ad91f6db9d)
![image](https://github.com/user-attachments/assets/9f423f94-88d3-4447-8ce0-dc458b384c3c)

5. Create Route Table

![image](https://github.com/user-attachments/assets/c151aadf-38f8-4e3a-9621-c38f063ade90)

6. Associate the RT to subnets which created in Step 5

![image](https://github.com/user-attachments/assets/a93116a9-0d0c-49b7-a68f-1973cfb1605c)
![image](https://github.com/user-attachments/assets/46d9236b-efc8-4403-938b-992e09f3b970)

7. Now the RT is associated with the subnets and this RT should have internet, edit the routes and add IGW to it for internet

![image](https://github.com/user-attachments/assets/f0f54c49-a489-41fc-b5ff-e86a7ccf648f)
![image](https://github.com/user-attachments/assets/e4da509d-582e-453d-8580-03f6da73674c)

8. Create a Target Group

Target Group is responsible for point to:
- Instances
- IP Addresses
- Lambda function
- Application Load Balancer

![image](https://github.com/user-attachments/assets/93718a79-b017-4190-8795-62125fe917c6)

- As of now there are no instances available, we are going to create instances through ASG.
9. Create the Load Balancer

Choose the Application Load Balancer and choose the below attributes:

 i. ALB
 
 ii. VPC
 
 iii. Subnets
 
 iv. Security Group (create a new SG to allow HTTP)
 
- When creating an Application Load Balancer (ALB) for internet access, we need to enable HTTP port 80, create a new security group, attach it to the VPC used for the Auto Scaling Group (ASG), and associate it with the ALB.

v. In listeners and routing - Select the Target Group

![image](https://github.com/user-attachments/assets/0a7f457a-27a1-488b-81fa-b98c20597767)

10. Create ASG (Auto Scaling Group)

![image](https://github.com/user-attachments/assets/1a2a1d5e-aaf3-4f70-84af-8ebc8b10fee9)

Step 1: Launch Template

- Give the name to Launch Template
- Choose the AMI, in this workaround I'm choosing Ubuntu
- No need to select the subnets for Auto Scaling Templates
- Select the key pair or create the new
- In Security Group : Create a Security Group to enable the port for HTTP (80) and SSH (22) and select the VPC
- Create the Launch Template
- In user data add to install Apache2

```bash
#!/bin/bash

yes | sudo apt update
yes | sudo apt install apache2
echo "<h1>Server Details</h1><p><strong>Hostname:</strong> $(hostname)</p><p><strong>IP Address:</strong> $(hostname -I | cut -d" " -f1)</p>" > /var/www/html/index.html
sudo systemctl restart apache2
```

Step 2:

- Select the VPC and availability zones and subnets

![image](https://github.com/user-attachments/assets/f21f95ca-9930-455b-9b46-14c3980d95f4)

Step 3:

- Select the existing Load Balancer
- Select the existing target group
- Enable the turn on Elastic Load Balancing health checks
- Choose the health check grace period

Step 4:

- Min: 1, Max: 3, Desired: 2
- If you want, you can choose the Scaling policy like "whenever the CPU utilization went to 75% an instance has to create"

Setp 5:
- Review all the steps and create ASG

Go to Load Balancer and choose the created LB and copy paste the dns name

![image](https://github.com/user-attachments/assets/cee08ea2-9bd5-448d-b390-47dc8814475e)

In the EC2 - Auto Scaling Group - Select the created ASG and check the "Instance Management" state.

![image](https://github.com/user-attachments/assets/12111f85-bd3c-4390-a9d6-32edff00e8d2)

- Now, we forcefully delete one of the EC2 instance and check whether the ASG will create another EC2 instance or not

![image](https://github.com/user-attachments/assets/81de7388-61b1-42aa-92a5-50b54f7be5c1)

![image](https://github.com/user-attachments/assets/acff314a-7e57-4da5-b60a-8c5c35250751)


We are Done! Happy Learning! :) ![image](https://github.com/user-attachments/assets/e9981724-a81c-42e6-a6ea-b5ef2c60ec93)
