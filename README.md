# ☁️ AWS Academy – Cloud Technical Essentials

> Labs, reports, and notes from the AWS Academy course.

**Course:** AWS Academy – Cloud Technical Essentials

---

## 📁 Repository Structure

```
aws-academy/
│
├── module-1-iam/
│   └── lab-1-introduction-to-iam/
│       ├── lab-report.md
│       └── screenshots/
│
├── lap 2/
│   ├── lab-report.md
│   └── screenshot/
│
├── lap 3/
│   ├── lab-report.md
│   └── screenshots/
│
├── Lap-4-main/
│   ├── lab-report 4.md
│   └── screenshots/
│
└── notes/
    └── general-aws-notes.md
```

---

## 🚀 Quick Access – Lab Reports

| Module | Lab | Report |
|--------|-----|--------|
| Week 1 – IAM & Security | Lab 1: Introduction to IAM | [📄 View Report](module-1-iam/lab-1-introduction-to-iam/lab-report.md) |
| Week 2 – Compute & Networking | Lab 2: Launching EC2 & Web App | [📄 View Report](lap%202/lab-report.md) |
| Week 3 – Storage & Databases | Lab 3: Configure S3 & DynamoDB | [📄 View Report](lap%203/lab-report.md) |
| Week 4 – Monitoring & Optimization | Lab 4: ALB & Auto Scaling | [📄 View Report](Lap-4-main/lab-report%204.md) |

---

## 📚 Course Modules

| # | Week | Status |
|---|------|--------|
| 1 | AWS Overview and Security (IAM) | ✅ Done |
| 2 | Compute & Networking (EC2 & VPC) | ✅ Done |
| 3 | Storage & Databases (S3 & DynamoDB) | ✅ Done |
| 4 | Monitoring & Optimization (ALB & Auto Scaling) | ✅ Done |

---

## 🧪 Labs

### Week 1 – AWS Overview and Security
- **[Lab 1: Introduction to IAM](module-1-iam/lab-1-introduction-to-iam/lab-report.md)**
  - Explored IAM users, groups, and policies
  - Managed user-to-group assignments (S3-Support, EC2-Support, EC2-Admin)
  - Tested permissions using the IAM sign-in URL
  - Verified the principle of least privilege across user-1, user-2, user-3

> 🔗 **Services used:** IAM

---

### Week 2 – Compute & Networking
- **[Lab 2: Launching an EC2 Instance & Deploying a Web Application](lap%202/lab-report.md)**
  - Reviewed VPC configuration: subnets, internet gateway, and route tables
  - Validated security group rules (HTTP port 80 / HTTPS port 443)
  - Launched a `t3.micro` EC2 instance with Amazon Linux 2023
  - Wrote and executed a **user data bootstrap script** to automate app deployment
  - Deployed a Node.js web application accessible via public IPv4

> 🔗 **Services used:** Amazon EC2, Amazon VPC, Security Groups, IAM Instance Profile

---

### Week 3 – Storage & Databases
- **[Lab 3: Configure a Web Application to use Amazon S3 & DynamoDB](lap%203/lab-report.md)**
  - Created an Amazon S3 bucket for employee photo storage
  - Applied an S3 bucket policy to grant the EC2 app access via `EmployeeDirectoryAppRole`
  - Configured the Employee Directory web app to use the S3 bucket
  - Uploaded 10 employee `.png` images to S3
  - Created a DynamoDB table (`Employees`) with partition key `id` (String)
  - Tested the app by adding new employee records through the web interface
  - Managed and edited DynamoDB items via the AWS Management Console

> 🔗 **Services used:** Amazon S3, Amazon DynamoDB, Amazon EC2, IAM

---

### Week 4 – Monitoring & Optimization
- **[Lab 4: Configure High Availability with ALB & Auto Scaling](Lap-4-main/lab-report%204.md)**
  - Reviewed EC2 instance and validated the Employee Directory web application
  - Created an **Application Load Balancer** (ALB) with a target group across 2 AZs
  - Created a **Launch Template** with user data script for automated app deployment
  - Set up an **EC2 Auto Scaling group** with desired capacity of 2, max of 4
  - Configured **Target Tracking Scaling Policy** at 30% CPU utilization
  - Stress tested the application and observed automatic horizontal scaling
  - Verified load balancing across Availability Zones

> 🔗 **Services used:** Amazon EC2, ALB, Auto Scaling, SNS, Amazon S3, DynamoDB

---

## 🔑 Key Concepts Covered

- **IAM** – Users, Groups, Policies, Roles, Least Privilege
- **EC2** – Instances, AMIs, Instance Types, User Data, Lifecycle
- **VPC** – Subnets, Internet Gateway, Route Tables, Security Groups, NACLs
- **S3** – Buckets, Objects, Bucket Policies, Access Control
- **DynamoDB** – NoSQL Tables, Partition Keys, Items, Attributes, CRUD operations
- **ELB** – Application Load Balancer, Target Groups, Health Checks, Listeners
- **Auto Scaling** – Launch Templates, Scaling Policies, Target Tracking
- **SNS** – Notifications, Subscriptions
- **Shared Responsibility Model** – AWS vs Customer responsibilities
- **Global Infrastructure** – Regions, Availability Zones, Edge Locations

---

## 🛠️ Tools & Environment

- AWS Academy Learner Lab
- AWS Management Console
- AWS CLI
- IAM Policy Simulator

---

## 📜 Certifications Target

- [ ] AWS Cloud Practitioner (CLF-C02)
- [ ] AWS Solutions Architect – Associate (SAA-C03)

---

## 📬 Contact

**GitHub:** [mosadiq22](https://github.com/mosadiq22)

---

<p align="center">Made with ☁️ during AWS Academy – Cloud Technical Essentials 2026</p>
