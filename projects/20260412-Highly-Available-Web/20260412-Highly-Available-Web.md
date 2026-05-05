# 🏗️ CDA02: Highly Available Web Architecture on AWS

## 📌 Overview

This project demonstrates the design and deployment of a highly available web architecture in AWS using core infrastructure services. The goal was to move beyond simply launching resources and instead focus on how each component contributes to availability, traffic control, and scalability.

The architecture uses an Application Load Balancer as the controlled entry point, distributes traffic across multiple Availability Zones, and leverages an Auto Scaling Group to maintain system reliability.

---

## 🧠 Architecture Summary

At a high level, the architecture follows this flow:
Internet → Application Load Balancer → EC2 Instances (Auto Scaling Group)

- Traffic enters through the load balancer  
- Requests are routed to healthy EC2 instances  
- Instances are distributed across multiple Availability Zones  
- Auto Scaling ensures a minimum number of instances are always running  

---

## 🧱 Services Used

- Amazon VPC  
- Subnets (Public)  
- Internet Gateway  
- Route Tables  
- Security Groups  
- EC2 (Amazon Linux)  
- Launch Template  
- Application Load Balancer (ALB)  
- Target Group  
- Auto Scaling Group (ASG)  

---

## 🌐 Network Configuration

- **VPC CIDR:** `10.10.0.0/16`  
- **Public Subnets:**
  - `10.10.1.0/24` (us-east-1a)  
  - `10.10.2.0/24` (us-east-1b)  
  - `10.10.3.0/24` (us-east-1c)  

- **Routing:**
  - `0.0.0.0/0 → Internet Gateway`

---

## 🔐 Security Design

### ALB-SG
- Allows inbound HTTP (port 80) from anywhere (`0.0.0.0/0`)

### Web-SG
- Allows inbound HTTP (port 80) **only from ALB-SG**

This ensures that:
- Users cannot access EC2 instances directly  
- All traffic must pass through the load balancer  

---

## ⚙️ Compute Configuration

### Launch Template
- Amazon Linux AMI  
- Instance type: `t2.micro`  
- Security group: Web-SG  

### User Data Script

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "LUIT with Comfort in the Cloud from $(hostname)" > /var/www/html/index.html
```


⚖️ Load Balancing & Scaling
Application Load Balancer
Internet-facing
Listens on HTTP (port 80)
Routes traffic to target group
Target Group
Registers EC2 instances
Performs health checks
Routes traffic only to healthy instances
Auto Scaling Group
Minimum: 2 instances
Maximum: 5 instances
Deployed across all three subnets
🧪 Validation
Accessed application using ALB DNS
Apache page loaded successfully
Hostname confirmed responses from EC2 instances
Refreshing showed traffic distribution
🔍 Key Takeaways
High availability comes from multi-AZ design
Load balancers control entry into the system
Security groups enforce access boundaries
Auto Scaling maintains system reliability
☁️ Behind-the-Scenes Discovery

AWS uses two ways to identify Availability Zones:

Public names (e.g., us-east-1a)
Internal IDs (e.g., use1-az1, use1-az4)

This can make it appear as though an extra zone exists, when it is simply a different internal labeling system.

📸 Architecture Diagram

## 📸 Architecture Diagram

![AWS Highly Available Web Architecture with ALB and Auto Scaling](projects/20260412-Highly-Available-Web/assets/CBentonCDA02WM2.png)

🔗 Related Write-Up

👉 [Medium Article](https://medium.com/@mrsceebenton2/building-a-highly-available-web-architecture-4c2997c7d5ae)

🚀 Future Improvements
Move EC2 instances to private subnets
Add HTTPS with ACM
Use Systems Manager Session Manager
Rebuild using Terraform
👩🏽‍💻 Author

Comfort Benton
Cloud Engineer

Still building. Always learning.
Still leaning into Comfort in the Cloud. ☁️

