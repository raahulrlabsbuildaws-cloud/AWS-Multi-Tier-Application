# AWS Multi-Tier Application Project

## 👤 Author
**Rahul Roy**
AWS Solutions Architect Associate (SAA-C03) | Cloud & Database Expert | 7 Years IT Experience

---

## 📌 Overview

This project demonstrates the design and deployment of a complete **Multi-Tier Web Application** on Amazon Web Services (AWS), following AWS best practices and security guidelines. The application is hosted in the **Asia Pacific (Mumbai) — ap-south-1** region and built entirely within the AWS Free Tier.

This is **Portfolio Project 1** in my AWS cloud portfolio, showcasing hands-on infrastructure skills beyond certification.

---

## 🏗️ Architecture Diagram

![AWS Multi-Tier Application Architecture](architecture-diagram.png)

The architecture follows a **3-tier model** separating the web server, database, and storage layers:

- **Internet** connects through an **Internet Gateway** into the VPC
- **EC2 (Web Server)** sits in the **Public Subnet** — accessible from the internet
- **RDS (Database)** sits in the **Private Subnet** — NOT accessible from the internet
- **Security Group** acts as a firewall controlling inbound traffic
- **S3, CloudWatch, and IAM** support storage, monitoring, and security

---

## ☁️ AWS Services Used

| Service | Purpose | Free Tier |
|---------|---------|-----------|
| **VPC** | Isolated network with public and private subnets | Always Free |
| **EC2 (t3.micro)** | Web server running Apache HTTP Server | Credits |
| **RDS MySQL 8.4 (db.t3.micro)** | Managed relational database in private subnet | Credits |
| **S3** | Object storage for application files | Credits |
| **CloudWatch** | Monitoring dashboard for EC2 and RDS metrics | Always Free |
| **IAM** | Role-based access control (EC2AppRole) | Always Free |
| **Internet Gateway** | Enables public internet access to VPC | Always Free |
| **Security Groups** | Firewall rules for HTTP, SSH, MySQL | Always Free |

---

## 🌐 Network Architecture

| Component | Value |
|-----------|-------|
| **VPC Name** | MyAppVPC |
| **VPC CIDR Block** | 10.0.0.0/16 |
| **Public Subnet** | 10.0.32.0/24 — ap-south-1a |
| **Private Subnet** | 10.0.33.0/24 — ap-south-1b |
| **Internet Gateway** | MyAppVPC-igw (Attached) |
| **Route Table** | Public subnet routed to Internet Gateway |

---

## 🔒 Security Configuration

### Security Group — MyAppSecurityGroup

| Rule | Protocol | Port | Source |
|------|----------|------|--------|
| HTTP | TCP | 80 | 0.0.0.0/0 |
| SSH | TCP | 22 | 0.0.0.0/0 |
| MySQL | TCP | 3306 | 0.0.0.0/0 |

### Security Best Practices Followed

- IAM user created instead of using root account
- RDS database placed in **private subnet** — not publicly accessible
- S3 bucket with **all public access blocked**
- IAM Role (EC2AppRole) used for EC2 — no hardcoded credentials
- SSH access via **PuTTY with key pair authentication** (.pem converted to .ppk)

---

## 💻 EC2 Web Server

| Setting | Value |
|---------|-------|
| **Instance Name** | MyWebServer |
| **AMI** | Amazon Linux 2023 |
| **Instance Type** | t3.micro |
| **Subnet** | Public Subnet (10.0.32.0/24) |
| **Web Server** | Apache HTTP Server (httpd) |
| **Connection Method** | PuTTY with SSH key authentication |
| **Key Pair** | MyAppKey (.pem → .ppk via PuTTYgen) |

### Apache Installation Commands (via PuTTY)

```bash
# Update system
sudo dnf update -y

# Install Apache
sudo dnf install -y httpd

# Start and enable Apache
sudo systemctl start httpd
sudo systemctl enable httpd

# Create web page
echo "<h1>Welcome to Rahul's AWS Application</h1>" | sudo tee /var/www/html/index.html

# Verify Apache is running
sudo systemctl status httpd
```

---

## 🗄️ RDS Database

| Setting | Value |
|---------|-------|
| **DB Identifier** | myappdb |
| **Engine** | MySQL 8.4 |
| **Instance Class** | db.t3.micro |
| **Subnet** | Private Subnet (10.0.33.0/24) |
| **Public Accessibility** | No (Security Best Practice) |
| **Multi-AZ** | No (Free Tier) |
| **Storage** | 20 GB gp2 |

---

## 🪣 S3 Storage

| Setting | Value |
|---------|-------|
| **Bucket Name** | rahul-app-storage-2026 |
| **Region** | ap-south-1 |
| **Public Access** | Blocked (Security Best Practice) |
| **Versioning** | Disabled |

---

## 📊 CloudWatch Monitoring

A **CloudWatch Dashboard (MyAppDashboard)** was created to monitor:

- **EC2 CPU Utilization** — tracks web server performance
- **RDS Database Connections** — tracks active database connections

---

## 🔑 IAM Role

| Setting | Value |
|---------|-------|
| **Role Name** | EC2AppRole |
| **Trusted Entity** | EC2 |
| **Policies Attached** | AmazonS3FullAccess, CloudWatchFullAccess |

The IAM role is attached directly to the EC2 instance — eliminating the need for hardcoded AWS credentials in the application.

---

## ✅ AWS Best Practices Applied

- ✅ **IAM User** used instead of root account for all operations
- ✅ **Public/Private Subnet** separation — web server public, database private
- ✅ **Security Group** with minimum required ports only
- ✅ **RDS in Private Subnet** — not directly accessible from internet
- ✅ **S3 Public Access Blocked** — secure object storage
- ✅ **IAM Role for EC2** — no hardcoded credentials anywhere
- ✅ **CloudWatch Monitoring** — full visibility into resource health
- ✅ **SSH Key Authentication** via PuTTY — industry standard secure access
- ✅ **MySQL 8.4** — latest LTS version (MySQL 8.0 reached end of support July 2026)
- ✅ **t3.micro** — latest generation free-tier instance (t2.micro deprecated)

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Subnet CIDR overlap with auto-created subnets | Used non-overlapping CIDR: 10.0.32.0/24 and 10.0.33.0/24 |
| EC2 Instance Connect blocked on new account | Used PuTTY with SSH key authentication instead |
| MySQL 8.0 reached end of support on RDS | Upgraded to MySQL 8.4 (new LTS version) |
| Public subnet not routing to internet | Explicitly associated Public-Subnet to the public route table |
| EC2 web page not loading | Fixed by associating correct subnet to route table with IGW route |

---

## 📸 Project Screenshots

| # | File | What It Shows |
|---|------|---------------|
| 01 | IAM-user-Raahhul.jpg | IAM user Raahhul-AWS-user with AdministratorAccess policy attached |
| 02 | VPC-1.jpg | VPC Dashboard showing all resources in ap-south-1 region |
| 03 | MyAppVPC.jpg | MyAppVPC resource map with subnets, route tables and network connections |
| 04 | Public_Private-Subnets.jpg | Both Public-Subnet (10.0.32.0/24) and Private-Subnet (10.0.33.0/24) listed |
| 05 | MyAppVPC-igw.jpg | MyAppVPC-igw Internet Gateway showing Attached status to MyAppVPC |
| 06 | MyAppSecurityGroup.jpg | MyAppSecurityGroup created successfully with description |
| 07 | MyAppSecurityGroup-inbound-rules.jpg | All 3 inbound rules — HTTP (80), MySQL/Aurora (3306), SSH (22) |
| 08 | MyWebServer-Ec2Instance.jpg | MyWebServer EC2 instance Running with Public IP 35.154.140.243 |
| 09 | Putty-Connected.jpg | PuTTY terminal connected to EC2 as ec2-user on Amazon Linux 2023 |
| 10 | Putty-terminal-showing-Apache-running.jpg | Apache httpd active (running) — server configured, listening on port 80 |
| 11 | Webserver-Connected.jpg | Web application accessible in browser at http://13.127.181.185 |
| 12 | MyAppDatabase.jpg | RDS myappdb showing Available status — MySQL, db.t3.micro, ap-south-1a |
| 13 | RaahhulApp2026-S3-Bucket.jpg | S3 bucket with RahulRoyCV2026.pdf uploaded (255.8 KB) |
| 14 | Cloudwatch-Dashboard.jpg | MyAppDashboard with CPUUtilization and DatabaseConnections widgets |
| 15 | Ec2AppRole_with2Poilices.jpg | EC2AppRole with AmazonS3FullAccess and CloudWatchFullAccess policies |

---

## 🎓 AWS Certification

| Detail | Value |
|--------|-------|
| **Certification** | AWS Solutions Architect Associate |
| **Exam Code** | SAA-C03 |
| **Score** | 874 / 1000 (Passing Score: 720) |
| **Certification ID** | AWS06184233 |
| **Valid Until** | August 2029 |
| **Domains Passed** | Security, Resilience, Performance, Cost Optimization |

---

## 📞 Connect With Me

- **AWS Certification ID:** AWS06184233
- **Experience:** 7 Years Enterprise IT
- **Skills:** AWS Cloud | Oracle DBA | MS SQL Server | Production Support
- **Location:** Kolkata, West Bengal, India
- **Open To:** AWS Solutions Architect | Cloud Engineer | Cloud DBA roles

---

*Built with hands-on AWS experience | Following AWS Well-Architected Framework principles*
