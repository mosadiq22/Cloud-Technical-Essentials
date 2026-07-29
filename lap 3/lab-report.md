# 🗄️ AWS S3 & DynamoDB Lab Report – Lab 3

| | |
|---|---|
| **Student** | Mohammed Alsadiq |
| **Course** | AWS Academy – Cloud Technical Essentials |
| **Lab** | Configure a Web Application to use Amazon S3 & DynamoDB |
| **Date** | July 2026 |

---

## Objective

The objective of this lab was to:

- Create an Amazon S3 bucket for employee photo storage.
- Create and apply an S3 bucket policy to grant application access.
- Configure the web application to use the S3 bucket.
- Upload objects (images) to the S3 bucket.
- Create an Amazon DynamoDB table to store employee data.
- Test the application using the web interface.
- Manage DynamoDB items via the AWS Management Console.

---

## Environment

- AWS Academy Learner Lab
- AWS Management Console
- EC2 instance hosting the Employee Directory web application
- IAM Role: `EmployeeDirectoryAppRole`
- Services used: Amazon S3, Amazon DynamoDB, Amazon EC2

---

## Task 1 – Create an Amazon S3 Bucket

### Procedure

1. Navigated to **S3** in the AWS Management Console.
2. Chose **Create bucket**.
3. Configured the bucket with the following settings:

| Setting | Value |
|---------|-------|
| Bucket Name | employee-photo-bucket-jwf-1988 |
| Region | us-west-2 |
| Block Public Access | Enabled (all public access blocked) |

4. Chose **Create bucket**.

### Result

Bucket created successfully.

### Screenshot

**Figure 1 – S3 Bucket Created**

![Figure 1](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%201.png)

---

## Task 2 – Create an S3 Bucket Policy

### Procedure

1. Opened the bucket → **Permissions** tab → **Bucket policy** → **Edit**.
2. Added the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3ReadAccess",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::885491962559:role/EmployeeDirectoryAppRole"
      },
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::employee-photo-bucket-jwf-1988",
        "arn:aws:s3:::employee-photo-bucket-jwf-1988/*"
      ]
    }
  ]
}
```

3. Replaced `ACCOUNT-ID` with the lab AWS Account ID.
4. Chose **Save changes**.

### Result

Bucket policy saved successfully — application can now access the S3 bucket via the `EmployeeDirectoryAppRole` IAM role.

### Screenshot

**Figure 2 – Bucket Policy Applied**

![Figure 2](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%202.png)

---

## Task 3 – Modify the Application to Use the S3 Bucket

### Procedure

1. Opened the Employee Directory web application.
2. Navigated to **Administration → Configuration**.
3. Chose **Change** in the S3 Bucket field.
4. Entered the bucket name: `employee-photo-bucket-jwf-1988`.
5. Chose **Save**.

### Result

Application successfully configured to use the S3 bucket. S3 Access Enabled indicator turned green.

### Screenshot

**Figure 3 – Application S3 Configuration**

![Figure 3](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%203.png)

---

## Task 4 – Upload Objects to the S3 Bucket

### Procedure

1. Downloaded the employee photos zip file from the lab.
2. Extracted the 10 `.png` image files.
3. Navigated to the S3 bucket → **Objects** tab → **Upload**.
4. Selected all 10 `.png` files and chose **Upload**.

### Result

All 10 employee images uploaded successfully. Images appeared in the application under **Employees → Images**.

### Screenshot

**Figure 4 – Images Uploaded to S3**

![Figure 4](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%204.png)

---

## Task 5 – Create an Amazon DynamoDB Table

### Procedure

1. Navigated to **DynamoDB** in the AWS Management Console.
2. Chose **Create table** with the following configuration:

| Setting | Value |
|---------|-------|
| Table Name | Employees |
| Partition Key | id (String) |

3. Chose **Create table** and waited for status to show **Active**.

### Result

DynamoDB table `Employees` created successfully with status **Active**.

### Screenshot

**Figure 5 – DynamoDB Table Created**

![Figure 5](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%205.png)

---

## Task 6 – Test the Application Using the Web Interface

### Procedure

1. Refreshed the Employee Directory application.
2. Confirmed the DynamoDB error was gone.
3. Navigated to **Employees → Management**.
4. Used **Actions → New Employee** to add a new employee record with:
   - Name, Location, Email
   - Selected a photo from the S3 bucket

### Result

New employee record created and displayed correctly in the application.

### Screenshot

**Figure 6 – New Employee Added via Web Interface**

![Figure 6](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%206.png)

---

## Task 7 – Manage DynamoDB Items via AWS Console

### Procedure

1. Returned to DynamoDB → **Tables → Employees**.
2. Chose **Explore table items**.
3. Selected an item by clicking the `id` link.
4. Edited the `location` and `email` fields in JSON view.
5. Chose **Save changes**.

### Result

Item updated successfully. Changes reflected immediately in the web application.

### Screenshot

**Figure 7 – Editing DynamoDB Item**

![Figure 7](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%207.png)

---

## Task 8 – Create Items via AWS Console

### Procedure

1. In DynamoDB → **Items returned** → **Create item**.
2. Added the following attributes in Form view:

| Attribute | Value |
|-----------|-------|
| id | 057b1086-d923-42e7-801b-39d9b8c930c2 |
| name | Mohamed |
| location | New York |
| email | mohamed@example.nyc |
| photo | employee-3.png |

3. Chose **Create item**.

### Result

Item saved successfully and appeared in the Employee Directory application.

### Screenshot

**Figure 8 – New Item Created in DynamoDB Console**

![Figure 8](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%208.png)

**Figure 9 – Employee Directory with New Item**

![Figure 9](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%209.png)

**Figure 10 – Final Application View**

![Figure 10](https://raw.githubusercontent.com/mosadiq22/aws-academy/master/lap%203/screenshots/task%2010.png)

---

## Summary

| Task | Description | Status |
|------|-------------|--------|
| 1 | Create S3 Bucket | ✅ Completed |
| 2 | Create S3 Bucket Policy | ✅ Completed |
| 3 | Configure App to Use S3 | ✅ Completed |
| 4 | Upload Images to S3 | ✅ Completed |
| 5 | Create DynamoDB Table | ✅ Completed |
| 6 | Test App via Web Interface | ✅ Completed |
| 7 | Manage Items via AWS Console | ✅ Completed |
| 8 | Create Items via AWS Console | ✅ Completed |

---

## Conclusion

This lab demonstrated how to integrate Amazon S3 and Amazon DynamoDB with a running EC2-hosted web application.

Key takeaways:
- **Amazon S3** provides scalable object storage for static assets like images.
- **S3 bucket policies** use IAM roles to grant fine-grained access to applications securely.
- **Amazon DynamoDB** is a fully managed NoSQL database ideal for storing structured application data.
- **IAM roles** allow EC2 instances to access AWS services without hardcoded credentials.
- Application data and storage can be managed both via the **web interface** and directly through the **AWS Management Console**.
