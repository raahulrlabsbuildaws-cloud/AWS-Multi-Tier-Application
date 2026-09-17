# AWS Multi-Tier Application Project ## Overview This project demonstrates hands-on AWS cloud
infrastructure knowledge. I built a complete multi-tier application on AWS Free Tier following AWS best
practices and security guidelines. ## Architecture ``` Internet fl Internet Gateway (MyAppIGW) fl Security
Group (MyAppSecurityGroup) - Firewall with 3 rules: HTTP/80, SSH/22, MySQL/3306 fl VPC
(MyAppVPC) - 10.0.0.0/16 nn Public Subnet (10.0.1.0/24) - ap-south-1a n nn EC2 Instance
(MyWebServer) - Web Server nn Private Subnet (10.0.2.0/24) - ap-south-1b nn RDS Database (myappdb) 
MySQL 8.0 Storage: S3 Bucket (rahul-app-2026-001) Monitoring: CloudWatch Dashboard
(MyAppDashboard) IAM Role: EC2AppRole (S3 + CloudWatch permissions) ``` ## Components Built ###
1. IAM User (Security Best Practice) - Created non-root IAM user 'rahul-aws-user' for project - Attached
AdministratorAccess policy - Followed AWS security best practice (never use root for daily work) ### 2.
VPC & Networking - VPC: MyAppVPC (10.0.0.0/16) - Public Subnet: 10.0.1.0/24 (ap-south-1a) - Private
Subnet: 10.0.2.0/24 (ap-south-1b) - Internet Gateway: MyAppIGW ### 3. Security - Security Group:
MyAppSecurityGroup with 3 inbound rules: - HTTP (Port 80) from 0.0.0.0/0 - SSH (Port 22) from 0.0.0.0/0 
MySQL (Port 3306) from 0.0.0.0/0 ### 4. Compute - EC2 Instance: MyWebServer (t2.micro, Amazon Linux
2) - Web server: Apache HTTP Server (httpd) - Public IP: [Your IP] - Status: Running ### 5. Database - RDS:
myappdb (MySQL 8.0, db.t2.micro) - Engine: MySQL - Status: Available - Location: Private subnet (not
publicly accessible) ### 6. Storage - S3 Bucket: rahul-app-2026-001 (ap-south-1) - Block all public access
enabled - Sample file uploaded ### 7. Monitoring - CloudWatch Dashboard: MyAppDashboard - Metrics
monitored: - EC2 CPU Utilization - RDS Database Connections ### 8. Access Control - IAM Role:
EC2AppRole - Policies: AmazonS3FullAccess, CloudWatchFullAccess ## Skills Demonstrated n AWS
Cloud Infrastructure Design n VPC Architecture & Networking n Security Groups & Network ACLs n EC2
Instance Management n RDS Database Setup & Configuration n S3 Object Storage n CloudWatch
Monitoring n IAM Roles & Permissions n AWS Best Practices (IAM user, security, monitoring) n
Linux/Bash Commands ## AWS Services Used - VPC (Virtual Private Cloud) - EC2 (Elastic Compute
Cloud) - RDS (Relational Database Service) - S3 (Simple Storage Service) - CloudWatch (Monitoring &
Logging) - IAM (Identity & Access Management) - Security Groups (Firewall) - Internet Gateway ## AWS
Certification - AWS Solutions Architect Associate (SAA-C03) - Certification ID: AWS06184233 - Score:
874/1000 - Valid until: August 2029 ## How to Replicate Follow the complete step-by-step guide provided in
the PDF to: 1. Create IAM user 2. Build VPC infrastructure 3. Launch EC2 web server 4. Create RDS
database 5. Set up S3 storage 6. Configure CloudWatch monitoring 7. Create IAM role Total time: ~3 hours
## Screenshots [15 screenshots of each step are included in the project] ## Project Timeline - Started:
September 5, 2026 - Completed: September 5, 2026 - Total time: 3 hours - AWS Free Tier used (no charges
incurred) ## Future Enhancements - Add Kubernetes orchestration (EKS) - Implement auto-scaling - Add
load balancer (ALB) - Set up CI/CD pipeline (CodePipeline) - Implement disaster recovery - Add cost
optimization ## Contact - GitHub: [github.com/raahulrlabsbuildaws-cloud] - LinkedIn: [https://www.linkedin.com/in/rahul-roy-4b351326a/] - Email: [raahul.rlabs.build.aws@gmail.com]
- AWS Cert: SAA-C03 (874/1000) --- **AWS Architecture & Infrastructure | Cloud & Database Expert | 7
Years IT Experience**
