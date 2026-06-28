# 🔐 AWS IAM Lab Report – Lab 1: Introduction to IAM

| | |
|---|---|
| **Student** | Mohammed Alsadiq |
| **Course** | AWS Academy |
| **Lab** | AWS Identity and Access Management (IAM) |
| **Date** | June 28, 2026 |

---

## Objective

The objective of this lab was to:

- Locate the IAM Sign-in URL.
- Sign in using different IAM users.
- Verify the permissions assigned to each user.
- Demonstrate the principle of least privilege by testing access to Amazon S3 and Amazon EC2.

---

## Environment

- AWS Academy Learner Lab
- AWS Management Console
- IAM Users: **user-1**, **user-2**, **user-3**

---

## Task 2 – Using the IAM Sign-in URL and Testing IAM User Permissions

### Task 2.1 – Locate the IAM Sign-in URL

#### Procedure

1. Opened the **IAM Dashboard**.
2. Located the **Sign-in URL for IAM users**.
3. Copied the URL for later use.

#### Result

The IAM Sign-in URL was successfully obtained.

#### Screenshot

**Figure 1 – IAM Dashboard showing the IAM Sign-in URL**

![Figure 1 – IAM Dashboard Sign-in URL](https://app.notion.com/p/AWS-IAM-Lab-Report-Lab-1-Introduction-to-IAM-38d2fbbadd2f80609479cc97b7341fb5?source=copy_link#38d2fbbadd2f80a5b0f9f159e445704e)

---

### Task 2.2 – Test IAM User Permissions

---

### Test 1 – user-1 (Amazon S3 Support)

#### Access to Amazon S3

**Steps**

- Logged in as **user-1**.
- Opened the Amazon S3 console.
- Accessed the lab S3 bucket.

**Result**

The user successfully viewed the S3 bucket and its contents.

**Figure 2 – user-1 accessing the S3 bucket**

![Figure 2 – user-1 S3 access](screenshots/fig2-user1-s3-access.png)

---

#### Access to Amazon EC2

**Steps**

- Opened the EC2 console.
- Navigated to **Instances**.

**Result**

Access was denied.

**Observed Error**

> You are not authorized to perform this operation.

This confirms that **user-1 does not have EC2 permissions**.

**Figure 3 – EC2 access denied for user-1**

![Figure 3 – user-1 EC2 denied](screenshots/fig3-user1-ec2-denied.png)

---

### Test 2 – user-2 (Amazon EC2 Read-Only Support)

#### Access to Amazon EC2

**Steps**

- Logged in as **user-2**.
- Opened EC2.
- Viewed the running instance.

**Result**

The instance information was visible.

---

#### Attempt to Stop the Instance

**Steps**

- Selected the EC2 instance.
- Chose **Instance State → Stop Instance**.

**Result**

The operation failed.

**Observed Error**

> You are not authorized to perform: ec2:StopInstances

This confirms that **user-2 has read-only permissions** and cannot modify EC2 resources.

**Figure 4 – Unauthorized error when stopping the instance**

![Figure 4 – user-2 stop instance denied](screenshots/fig4-user2-stop-denied.png)

---

#### Access to Amazon S3

**Steps**

- Opened the Amazon S3 console.

**Result**

No accessible buckets were displayed.

This confirms that **user-2 has no permissions for Amazon S3**.

**Figure 5 – Empty S3 bucket list for user-2**

![Figure 5 – user-2 S3 empty](screenshots/fig5-user2-s3-empty.png)

---

### Test 3 – user-3 (Amazon EC2 Administrator)

#### Access to Amazon EC2

**Steps**

- Logged in as **user-3**.
- Opened EC2.
- Selected the running instance.
- Chose **Instance State → Stop Instance**.

**Result**

The operation completed successfully. The EC2 instance entered the **Stopping** state and then **Stopped**.

This confirms that **user-3 has administrative permissions for Amazon EC2**.

**Figure 6 – EC2 instance successfully stopping**

![Figure 6 – user-3 EC2 stopping](screenshots/fig6-user3-ec2-stopping.png)

---

## Summary of Permissions

| IAM User | Amazon S3    | View EC2   | Stop EC2   |
|----------|--------------|------------|------------|
| user-1   | ✅ Allowed   | ❌ Denied  | ❌ Denied  |
| user-2   | ❌ Denied    | ✅ Allowed | ❌ Denied  |
| user-3   | ❌ Not Tested| ✅ Allowed | ✅ Allowed |

---

## Conclusion

This lab demonstrated the implementation of AWS IAM policies using the principle of least privilege.

- **user-1** was granted access only to Amazon S3.
- **user-2** was granted read-only access to Amazon EC2.
- **user-3** was granted administrative permissions for Amazon EC2 and successfully stopped the running instance.

The results verify that IAM policies effectively restrict users to only the actions explicitly permitted by their assigned roles.
