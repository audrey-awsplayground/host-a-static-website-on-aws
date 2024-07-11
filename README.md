![Alt text](/Host_a_Static_Website_on_AWS.png)

---

# Hosting a Static Website on AWS

This project demonstrates the deployment of a static HTML web application on AWS using various services for scalability, reliability, and security.

## Architecture Overview

1. **Virtual Private Cloud (VPC):** Configured a VPC with public and private subnets across two availability zones for network isolation and redundancy.

2. **Internet Gateway:** Deployed an Internet Gateway to enable communication between VPC instances and the internet.

3. **Security Groups:** Established Security Groups acting as firewalls to control inbound and outbound traffic to instances.

4. **Availability Zones:** Utilized multiple Availability Zones to enhance system availability and fault tolerance.

5. **Subnets:** Public subnets were used for resources like NAT Gateway and Application Load Balancer. Private subnets hosted web servers (EC2 instances) for enhanced security.

6. **EC2 Instance Connect:** Implemented EC2 Instance Connect for secure SSH connections to instances within both public and private subnets.

7. **NAT Gateway:** Enabled private subnet instances to access the internet via NAT Gateway while remaining private.

8. **Web Server Deployment:** Hosted the static website files on EC2 instances deployed in private subnets.

9. **Application Load Balancer (ALB):** Utilized ALB with a target group to distribute web traffic evenly across an Auto Scaling Group of EC2 instances in multiple AZs.

10. **Auto Scaling Group:** Managed EC2 instances automatically to ensure website availability, scalability, fault tolerance, and elasticity.

11. **Version Control and Collaboration:** Stored website files on GitHub for version control and collaboration.

12. **Certificate Manager:** Secured application communications using certificates managed by AWS Certificate Manager (ACM).

13. **Simple Notification Service (SNS):** Configured SNS to send notifications about activities within the Auto Scaling Group.

14. **Domain Name and DNS:** Registered a domain name and set up DNS records using Amazon Route 53.

## Deployment Script

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone [https://github.com/audrey-awsplayground/host-a-static-website-on-aws.git]
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Getting Started

To deploy this project on AWS, follow these steps:

1. **Prerequisites:**
   - AWS account with appropriate permissions.
   - Clone the repository from GitHub.

2. **Configuration:**
   - Update variables and configurations in AWS services (VPC, Security Groups, Route 53, etc.) based on your specific requirements.

3. **Deployment:**
   - Execute the provided deployment script on an EC2 instance.
   - Monitor deployment progress through AWS Management Console and CloudWatch.

4. **Testing:**
   - Access your static website using the registered domain name.
   - Verify load balancing, auto-scaling behavior, and overall functionality.

## Additional Notes

- For ongoing maintenance and updates, ensure to manage AWS resources securely and efficiently.
- Regularly monitor AWS services and set up alarms for critical metrics to maintain high availability.

---

Sources: I followed a step-by-step guide from aosnote.com to complete my first AWS DevOps project.
