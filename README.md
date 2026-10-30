# 🚀 AWS Three-Tier Web Application

### A hands-on AWS project by Mayur Chaudhari

![AWS](https://img.shields.io/badge/AWS-Cloud%20Project-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Architecture](https://img.shields.io/badge/Architecture-3--Tier-2563EB?style=for-the-badge)
![Region](https://img.shields.io/badge/Region-ap--south--1-16A34A?style=for-the-badge)

**Build • Secure • Scale • Learn**

## 📌 Project Overview

This project demonstrates a three-tier architecture on AWS. Each layer has a separate responsibility and security boundary.

| Layer | Technology | Responsibility | Network |
|---|---|---|---|
| 🌐 Web Tier | Nginx | Serves frontend and forwards API requests | Public subnets |
| ⚙️ App Tier | Node.js + PM2 | Handles application logic on port 4000 | Private subnets |
| 🗄️ Database Tier | Amazon Aurora MySQL | Stores transaction data on port 3306 | Private DB subnets |

## 🏗️ Architecture Diagram

![AWS Three-Tier Architecture](architecture-diagram.png)

Architecture: custom VPC 10.0.0.0/16, two Availability Zones, public web subnets, private app and database subnets, load balancers, NAT Gateways, S3 and IAM.

## 🔄 How the Application Works

1. A user opens the External Load Balancer DNS name in a browser.
2. The external load balancer forwards the request to a healthy Nginx web server.
3. Nginx serves the frontend. Requests beginning with /api are forwarded to the Internal Load Balancer.
4. The internal load balancer sends the request to a healthy Node.js server on port 4000.
5. Node.js reads or writes transaction data in Aurora MySQL on port 3306.
6. The response returns to the user's browser.

## 🧰 AWS Services and Technologies

| Service / Tool | Purpose |
|---|---|
| Amazon VPC | Isolated cloud network |
| Public and Private Subnets | Separates internet-facing and internal resources |
| Internet Gateway | Internet connectivity for public subnets |
| NAT Gateways | Outbound internet access for private resources |
| Route Tables | Control network traffic paths |
| Security Groups | Control inbound traffic between tiers |
| Amazon EC2 | Hosts web and application servers |
| Application Load Balancer | Distributes incoming traffic |
| Auto Scaling Groups | Maintains and scales EC2 capacity |
| Amazon Aurora MySQL | Stores application transactions |
| Amazon S3 | Stores application code |
| AWS IAM | Manages permissions |
| Systems Manager Session Manager | Connects to instances without SSH keys |
| Nginx | Serves frontend files and reverse-proxies API requests |
| Node.js + PM2 | Runs and manages the backend application |

## 🌐 Network Design

- **VPC CIDR:** 10.0.0.0/16
- **AWS Region:** Asia Pacific (Mumbai) — ap-south-1
- **Availability Zones:** Two

| Subnet | Availability Zone | CIDR | Type |
|---|---|---|---|
| Web-Tier-Subnet-1 | AZ 1a | 10.0.1.0/24 | Public |
| App-Tier-Subnet-1 | AZ 1a | 10.0.2.0/24 | Private |
| DB-Tier-Subnet-1 | AZ 1a | 10.0.3.0/24 | Private |
| Web-Tier-Subnet-2 | AZ 1b | 10.0.4.0/24 | Public |
| App-Tier-Subnet-2 | AZ 1b | 10.0.5.0/24 | Private |
| DB-Tier-Subnet-2 | AZ 1b | 10.0.6.0/24 | Private |

## 🔐 Security Group Traffic Flow

| Security Group | Inbound Port | Allowed Source |
|---|---|---|
| External Load Balancer SG | 80 | 0.0.0.0/0 |
| Web Tier SG | 80 | External Load Balancer SG |
| Internal Load Balancer SG | 80 | Web Tier SG |
| App Tier SG | 4000 | Internal Load Balancer SG |
| DB Tier SG | 3306 | App Tier SG |

> Each tier accepts traffic only from the tier directly in front of it. The database is not publicly accessible.

## 🚀 Project Implementation Steps

1. Create the VPC and six subnets across two Availability Zones.
2. Configure Internet Gateway, NAT Gateways and route tables.
3. Create security groups for all tiers.
4. Create the Aurora MySQL DB subnet group and database.
5. Create the EC2 IAM role and required permissions.
6. Create an S3 bucket and upload application code.
7. Configure and test the application server with Node.js and PM2.
8. Create the application server AMI.
9. Configure the app target group, launch template and internal load balancer.
10. Configure the web server, Nginx reverse proxy and frontend build.
11. Create the web server AMI.
12. Configure the web target group, launch template and external load balancer.
13. Create Auto Scaling Groups for web and app tiers.
14. Open the external load balancer DNS and test the application.

## ✅ Testing Checklist

- [ ] Frontend opens using the External Load Balancer DNS name.
- [ ] Nginx serves the frontend successfully.
- [ ] API requests reach the application tier.
- [ ] Node.js responds on port 4000.
- [ ] Database connectivity works on port 3306.
- [ ] Transaction records are displayed.
- [ ] Add and delete transaction operations work.
- [ ] Load balancer target groups show healthy targets.

## 🛡️ Production Security Notes

- Store database credentials in AWS Secrets Manager or SSM Parameter Store.
- Never commit secrets to GitHub.
- Use a restricted database user for the application.
- Configure HTTPS using AWS Certificate Manager.
- Keep the database private.
- Prefer Session Manager and keep SSH port 22 closed.
- Apply least-privilege IAM permissions.
- Enable encryption, backups, monitoring, logging and alerts.
- Use a supported Node.js LTS version.
- Consider Infrastructure as Code and CI/CD.

## 💰 AWS Cost Warning

AWS resources may incur charges even when the application is not actively being used.

Pay special attention to:

- NAT Gateways
- Aurora database
- Application Load Balancers
- EC2 instances
- Elastic IP addresses
- EBS snapshots and AMIs

After completing the lab, review your AWS resources and Billing console. Delete resources carefully and confirm that no billable lab resources remain.

## 📚 Learning Outcomes

- Designing a VPC across multiple Availability Zones
- Separating public and private tiers
- Configuring route tables, gateways and security groups
- Launching EC2 instances and creating AMIs
- Configuring Application Load Balancers
- Using Launch Templates and Auto Scaling Groups
- Connecting Node.js to Aurora MySQL
- Using S3 and IAM roles
- Accessing private instances through Session Manager

## 📄 Detailed Project Documentation

[📥 Open / Download the 3-Tier Project PDF](3-Tier-Doc-By-Mayurchaudhari.pdf)

> Keep README.md, architecture-diagram.png, and 3-Tier-Doc-By-Mayurchaudhari.pdf in the repository root folder so both links work.

---

### ⭐ Thank You for Visiting This Project!

**Project by Mayur Chaudhari**

*Learning AWS • Building Cloud Skills • Growing in DevOps*
