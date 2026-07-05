# 🖥️ AWS EC2 Lab Report – Lab 2: Introduction to EC2

| | |
|---|---|
| **Student** | Mohammed Alsadiq |
| **Course** | AWS Academy – Cloud Technical Essentials |
| **Lab** | Launching an EC2 Instance and Deploying a Web Application |
| **Date** | July 5, 2026 |

---

## Objective

The objective of this lab was to:

- Understand Amazon VPC configuration.
- Validate Subnet and Internet Gateway infrastructure.
- Confirm a Route Table has a public route to the internet.
- Review Security Group rules.
- Launch an Amazon EC2 instance.
- Configure an EC2 instance to host a web application using a user data script.

---

## Environment

- AWS Academy Learner Lab
- AWS Management Console
- Region: us-west-2
- VPC: Lab VPC (10.10.0.0/16)
- Subnet: lab-2-public-subnet-1 (10.10.1.0/24)
- Security Group: WebAppSG
- Instance Type: t3.micro
- AMI: Amazon Linux 2023

---

## Task 1 – Understand VPC Configuration

### Procedure

1. Navigated to **VPC** in the AWS Management Console.
2. Selected **Lab VPC** and reviewed its configuration.
3. Reviewed the subnet **lab-2-public-subnet-1**.
4. Reviewed the route table **lab-2-rtb-public**.

### Key Configurations Observed

| Setting | Value |
|---------|-------|
| IPv4 CIDR | 10.10.0.0/16 |
| IPv6 CIDR | None |
| DNS Resolution | Enabled |
| DNS Hostnames | Enabled |
| Subnet CIDR | 10.10.1.0/24 |
| Route Table Routes | Local, Internet Gateway, S3 Endpoint |

### Result

VPC configuration confirmed — internet gateway and route table correctly configured for public subnet access.

### Screenshot

**Figure 1 – Lab VPC Configuration**

![Figure 1 – Lab VPC](screenshots/fig1-vpc-config.png)

---

## Task 2 – Review VPC Security Group

### Procedure

1. Navigated to **Security Groups** in the VPC console.
2. Selected **WebAppSG** and reviewed its rules.

### Inbound Rules

| Port | Protocol | Source | Purpose |
|------|----------|--------|---------|
| 80 | TCP | 0.0.0.0/0 | Allow HTTP |
| 443 | TCP | 0.0.0.0/0 | Allow HTTPS |

### Outbound Rules

| Port | Protocol | Destination | Purpose |
|------|----------|-------------|---------|
| All | All | VPC Endpoints SG | Allow AWS service access |
| All | All | S3 Prefix List | Allow S3 access |

### Result

Security group correctly configured to allow HTTP/HTTPS inbound and necessary outbound traffic.

### Screenshot

**Figure 2 – WebAppSG Inbound Rules**

![Figure 2 – Security Group](screenshots/fig2-security-group.png)

---

## Task 3 – Launch EC2 Instance

### Instance Configuration

| Setting | Value |
|---------|-------|
| Name | Web Application |
| AMI | Amazon Linux 2023 |
| Architecture | 64-bit (x86) |
| Instance Type | t3.micro |
| Key Pair | None (Proceed without key pair) |
| VPC | Lab VPC |
| Subnet | lab-2-public-subnet-1 |
| Auto-assign Public IP | Enabled |
| Security Group | WebAppSG |
| IAM Instance Profile | LabInstanceProfile |

### User Data Script

```bash
#!/bin/bash -xe

# Installs Node.js
dnf install nodejs24 nodejs24-npm -y

# Downloads an NPM cache from S3 to aid package installation
aws s3 cp s3://npm-us-west-2-8257409892/npm-cache.tar.gz \
/var/cache/npm-cache.tar.gz

# Extracts the cache to a directory
mkdir -p /root/.npm
tar xzf /var/cache/npm-cache.tar.gz -C /root/.npm/

# Downloads the web app code as a zip file
mkdir -p /var/app/
aws s3 cp s3://npm-us-west-2-8257409892/app.zip \
/var/app/app.zip

# Extracts the web app zip to a directory
unzip /var/app/app.zip -d /var/app/

# Runs an offline npm install for needed packages
cd /var/app
npm install --offline

# Starts the Node.js web app
npm start
```

### Result

Instance launched successfully.

- **Instance State:** Running
- **Status Check:** 3/3 checks passed
- **Public IPv4:** assigned and accessible

### Screenshot

**Figure 3 – EC2 Instance Running (3/3 checks passed)**

![Figure 3 – Instance Running](screenshots/fig3-instance-running.png)

---

## Task 4 – Access the Web Application

### Procedure

1. Copied the **Public IPv4 address** from the instance details.
2. Opened a browser and navigated to `http://<Public-IP>`.

### Result

The web application loaded successfully over HTTP on port 80.

### Screenshot

**Figure 4 – Web Application Running in Browser**

![Figure 4 – Web App](screenshots/fig4-webapp-running.png)

---

## Summary

| Task | Status |
|------|--------|
| VPC Configuration Review | ✅ Completed |
| Security Group Review | ✅ Completed |
| EC2 Instance Launch | ✅ Completed |
| Web Application Deployment | ✅ Completed |

---

## Conclusion

This lab demonstrated how to launch an EC2 instance inside a properly configured VPC and deploy a Node.js web application using a user data bootstrap script.

Key takeaways:
- A **public subnet** with an **internet gateway** allows EC2 instances to be publicly accessible.
- **Security groups** act as virtual firewalls controlling inbound and outbound traffic.
- **User data scripts** automate application setup at instance launch time.
- The **IAM instance profile** grants the EC2 instance permission to access S3 without hardcoded credentials.
