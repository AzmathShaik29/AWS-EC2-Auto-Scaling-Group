# AWS Auto Scaling Group
An AWS Auto Scaling Group (ASG) is a feature that automatically manages the number of Amazon EC2 instances based on defined scaling policies, ensuring high availability and cost efficiency.

**Key Features of ASG:**
1. **Automatic Scaling:** Increases or decreases the number of EC2 instances based on CPU utilization, memory usage, or other metrics.
2. **Health Checks & Auto-Replacement:** Automatically replaces unhealthy instances to maintain system reliability.
3. **Load Balancer Integration:** Works with Elastic Load Balancer (ELB) to distribute traffic across instances.
Multiple Scaling Policies:
4. **Target Tracking Scaling:** Adjusts instances based on a target metric (e.g., keep CPU at 75% utilization).
5. **Step Scaling:** Adds or removes instances based on predefined step changes.
6. **Scheduled Scaling:** Launches or terminates instances at specific times.

**How ASG Works:**
1. **Define a Launch Template or Launch Configuration:** Specifies the instance type, AMI, key pair, security groups, and other settings.
2. **Create an Auto Scaling Group:** Defines the minimum, maximum, and desired number of instances.
3. **Set Scaling Policies:** Configures rules to automatically add or remove instances.
4. **Monitor and Adjust:** ASG continuously monitors metrics and adjusts the number of instances as needed.

# VPC
An Amazon Virtual Private Cloud (VPC) is a logically isolated network within AWS where you can launch and manage AWS resources securely. It gives you complete control over network configurations, including IP addressing, subnets, route tables, and security settings.

# IGW
An Internet Gateway (IGW) in AWS is a highly available and scalable component that allows instances in a public subnet of an Amazon Virtual Private Cloud (VPC) to communicate with the internet. It enables inbound and outbound traffic to and from the internet.

# Subnets
A Subnet is a logical division of a VPC that allows you to separate and manage resources efficiently. Each subnet is associated with a route table.

**Types of Subnets:**
- Public Subnet: Has a route to an Internet Gateway (IGW) → Instances can be accessed from the internet.
- Private Subnet: Does not have a direct route to the internet → Requires NAT Gateway for outbound internet access.
- Isolated Subnet: No internet access (internal workloads only).

# Route Tables
A Route Table in AWS defines how network traffic is directed within a VPC. It contains a set of routes (rules) that determine where traffic should be sent.

**Key Features:**
- Every VPC has a default route table.
- Each subnet in a VPC must be associated with a route table.
- Routes can point to different destinations like:
  - _Local (VPC Internal Traffic):_ 10.0.0.0/16 → local
  - _Internet Gateway (IGW) (Public Traffic):_ 0.0.0.0/0 → IGW
  - _NAT Gateway (Private Subnet Access to Internet):_ 0.0.0.0/0 → NAT Gateway
  - _VPC Peering, VPN, or Direct Connect_


# Target Group
A Target Group is used in AWS Elastic Load Balancer (ELB) to route traffic to specific EC2 instances, Lambda functions, or containers.

# Load Balancer
An AWS Load Balancer is a service that distributes incoming network traffic across multiple targets (EC2 instances, containers, or Lambda functions) to ensure high availability and fault tolerance.

![image](https://github.com/user-attachments/assets/028ebed4-9e0f-49be-aa62-c7749c35a5d0)
