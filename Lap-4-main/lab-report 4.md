# ⚖️ AWS High Availability Lab Report – Lab 4

| | |
|---|---|
| **Student** | Mohammed Alsadiq |
| **Course** | AWS Academy – Cloud Technical Essentials |
| **Lab** | Configure High Availability for Your Application |
| **Date** | August 2026 |

---

## Objective

The objective of this lab was to:

- Review an EC2 instance and validate the web application configuration.
- Create an Application Load Balancer (ALB) and target group.
- Create a Launch Template for Auto Scaling.
- Set up an EC2 Auto Scaling group.
- Stress test the application to validate horizontal scaling.

---

## Environment

- AWS Academy Learner Lab
- AWS Management Console
- Region: us-west-2
- VPC: Lab VPC
- Subnets: Public Subnet 1 & Public Subnet 2 (two Availability Zones)
- Services used: Amazon EC2, ALB, Auto Scaling, SNS, S3, DynamoDB

---

## Task 1 – Review EC2 Instance & Web Application

### Procedure

1. Navigated to **EC2 → Instances**.
2. Selected the **Web Application** instance (Running state).
3. Copied **PublicWebApplicationURL** and opened the application.
4. Navigated to **Administration → Configuration** and noted the Availability Zone.

### Result

Web application confirmed running on a single EC2 instance in one Availability Zone.

### Screenshot

**Figure 1 – Web Application Running**

![Figure 1](screenshots/Web%20Application%20Running%201.png)

---

## Task 2 – Create an Application Load Balancer

### Procedure

1. Navigated to **EC2 → Load Balancers → Create Load Balancer → Application Load Balancer**.
2. Configured the ALB:

| Setting | Value |
|---------|-------|
| Name | Web-Application-ALB |
| VPC | Lab VPC |
| Availability Zones | Both AZs selected |
| Security Group | LoadBalancerSG |

3. Created a target group with the following settings:

| Setting | Value |
|---------|-------|
| Type | Instances |
| Name | lab-app-target-group |
| Healthy threshold | 2 |
| Unhealthy threshold | 5 |
| Timeout | 20 seconds |
| Interval | 30 seconds |

4. Registered the **Web Application** instance as a pending target.
5. Linked `lab-app-target-group` to the ALB listener.
6. Chose **Create load balancer**.
7. Copied the **DNS name** and verified the application loads over HTTP.

### Result

ALB created successfully with status **Active**. Employee Directory application accessible via ALB DNS name.

### Screenshot

**Figure 2 – Create Application Load Balancer**
![Figure 2](screenshots/Create%20an%20Application%20Load%20Balancer%202.png)

**Figure 3 – Target Group Created**
![Figure 3](screenshots/target%20group%202.png)

**Figure 4 – Create Load Balancer**
![Figure 4](screenshots/Create%20load%20balancer%202.png)

**Figure 5 – ALB Active**
![Figure 5](screenshots/ALB%20Active%202.png)



---

## Task 3 – Create a Launch Template

### Procedure

1. Navigated to **EC2 → Launch Templates → Create launch template**.
2. Configured the template:

| Setting | Value |
|---------|-------|
| Name | lab-app-launch-template |
| Description | A web server for the employee directory app |
| AMI | Amazon Linux 2023 (64-bit x86) |
| Instance type | t3.micro |
| Key pair | Don't include |
| Security group | LoadBalancerSG |
| IAM instance profile | EmployeeDirectoryAppRole |
| Metadata version | V1 and V2 |

3. Added user data script with the following variables configured:
   - `IMAGES_BUCKET` → ImagesBucket value from lab
   - `INSTALLATION_BUCKET` → InstallationBucket value from lab
   - `YOUR_DEFAULT_AWS_REGION` → us-west-2

4. Chose **Create launch template**.

### Result

Launch template `lab-app-launch-template` created successfully.

### Screenshot

**Figure 6 – Launch Template Created**

![Figure 6](screenshots/Launch%20Template%20Created%203.png)

---

## Task 4 – Create an Auto Scaling Group

### Procedure

1. Navigated to **EC2 → Auto Scaling Groups → Create Auto Scaling group**.
2. Configured the group:

| Setting | Value |
|---------|-------|
| Name | app-asg |
| Launch template | lab-app-launch-template |
| VPC | Lab VPC |
| Subnets | Public Subnet 1 + Public Subnet 2 |
| Load balancer | lab-app-target-group \| HTTP |
| ELB health checks | Enabled |
| Desired capacity | 2 |
| Minimum capacity | 2 |
| Maximum capacity | 4 |
| Scaling policy | Target tracking |
| Target value (CPU) | 30% |
| Instance warmup | 300 seconds |

3. Created SNS notification topic `lab-app-sns-topic` and confirmed email subscription.
4. Chose **Create Auto Scaling group**.
5. Verified 2 instances launched and showing **healthy** in the target group.
6. Terminated the original **Web Application** EC2 instance.
7. Confirmed application still accessible via ALB DNS after termination.

### Result

Auto Scaling group `app-asg` created with 2 healthy instances across two Availability Zones. Original instance terminated without downtime.

### Screenshot

**Figure 7 – Auto Scaling Group Created**
![Figure 7](screenshots/Create%20Auto%20Scaling%20group%204.png)

**Figure 8 – Delete Web Application**
![Figure 8](screenshots/4%20delete%20web%20application.png)

**Figure 9 – Auto Scaling Groups**
![Figure 9](screenshots/Auto%20Scaling%20groups%204.png)


---

## Task 5 – Stress Test & Validate Scaling

### Procedure

1. Opened the application via the ALB DNS name.
2. Navigated to **Administration → Configuration**.
3. Refreshed the page multiple times — observed the **Availability Zone changing** confirming load balancing is working.
4. In **Admin Tools**, selected **Stress Application Server For: 10 minutes**.
5. After ~10 minutes, navigated to **Target Groups → lab-app-target-group → Targets**.
6. Observed new instances being provisioned automatically.
7. Received SNS email notification about the scaling event.

### Result

- ✅ Load balancing confirmed — traffic routed across both AZs
- ✅ Auto scaling triggered — new instances added during CPU stress
- ✅ SNS notification received for scaling event

### Screenshot

**Figure 11 – Load Balancing Across AZs**
![Figure 11](screenshots/5.%20Load%20Balancing%20Across%20AZs.png)

**Figure 12 – Monitoring the Performance**
![Figure 12](screenshots/5.montiring%20the%20preformance.png)

---

## Summary

| Task | Description | Status |
|------|-------------|--------|
| 1 | Review EC2 Instance & Web Application | ✅ Completed |
| 2 | Create Application Load Balancer | ✅ Completed |
| 3 | Create Launch Template | ✅ Completed |
| 4 | Create Auto Scaling Group | ✅ Completed |
| 5 | Stress Test & Validate Scaling | ✅ Completed |

---

## Conclusion

This lab demonstrated how to configure high availability and horizontal scaling for a web application on AWS.

Key takeaways:
- **Application Load Balancer** distributes traffic across multiple EC2 instances and Availability Zones, eliminating single points of failure.
- **Launch Templates** standardize EC2 instance configuration for consistent deployments.
- **Auto Scaling Groups** automatically adjust the number of instances based on CPU load, ensuring performance under demand.
- **Target tracking scaling policies** maintain a target CPU utilization (30%) by scaling in or out as needed.
- **Health checks** ensure traffic is only sent to healthy instances, and unhealthy ones are automatically replaced.
- **SNS notifications** provide real-time alerts for scaling events.
