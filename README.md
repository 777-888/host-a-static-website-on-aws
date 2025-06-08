# Host a Static Website on AWS

This project demonstrates how to host a static HTML website on AWS by deploying and configuring key infrastructure components using EC2 and other AWS services. This setup ensures high availability, fault tolerance, and scalability using best practices in cloud architecture.

## 📌 Project Overview

I recently completed a DevOps project where I hosted a static website on AWS. This repository includes:
- A reference architecture diagram
- Bash scripts for EC2 provisioning and configuration
- Step-by-step documentation of the infrastructure setup

## 🛠️ AWS Services Used

1. **VPC Configuration**: Created a Virtual Private Cloud (VPC) with both public and private subnets across two Availability Zones (AZs).
2. **Internet Gateway**: Enabled internet connectivity for resources within the VPC.
3. **Security Groups**: Configured as virtual firewalls to control inbound and outbound traffic to resources.
4. **Multi-AZ Setup**: Leveraged two AZs for high availability and fault tolerance.
5. **Public Subnets**: Used for resources like NAT Gateway and Application Load Balancer (ALB).
6. **EC2 Instance Connect Endpoint**: Enabled secure access to both public and private subnet resources.
7. **Private Subnets**: Hosted EC2 web servers for better security.
8. **NAT Gateway**: Allowed instances in private subnets to access the internet for updates and Git operations.
9. **EC2 Instances**: Hosted the actual website content.
10. **Application Load Balancer (ALB)**: Distributed traffic across EC2 instances.
11. **Auto Scaling Group**: Ensured elasticity, scalability, and high availability of EC2 instances.
12. **GitHub**: Used for version control and collaborative development of the web content.
13. **AWS Certificate Manager**: Secured web traffic with HTTPS.
14. **SNS (Simple Notification Service)**: Configured to send alerts related to the Auto Scaling Group.
15. **Route 53**: Managed the custom domain and DNS routing.

## 📂 Project Structure

- `infrastructure/` – Terraform (or other IaC) templates (if applicable)
- `scripts/` – Shell scripts used for bootstrapping EC2 instances
- `diagrams/` – Architecture diagrams and network layout
- `website/` – HTML/CSS/JS files for the static website

## 🚀 EC2 User Data Script

This script bootstraps an Amazon Linux EC2 instance to install and run a static website using Apache and GitHub:

```bash
#!/bin/bash
# Switch to the root user
sudo su

# Update system packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Install Git
yum install -y git

# Navigate to the Apache root directory
cd /var/www/html

# Clone the GitHub repository containing the website files
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all website files into the web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Clean up
rm -rf host-a-static-website-on-aws

# Enable and start the Apache service
systemctl enable httpd
systemctl start httpd

🔐 Note: Ensure proper IAM roles and security groups are configured to allow HTTP access and secure GitHub cloning.

🌐 Domain and DNS

Registered a custom domain name via Route 53
Set up DNS routing to point to the Load Balancer
📎 Additional Notes

This project is designed with scalability and real-world reliability in mind.
Monitoring, alerting, and secure deployment practices are incorporated where possible.
