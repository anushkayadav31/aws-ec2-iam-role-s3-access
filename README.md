# AWS EC2 IAM Role-Based S3 Access

## 📌 Project Overview

This project demonstrates secure access between an Amazon EC2 instance and an Amazon S3 bucket using an IAM Role.

An AWS-managed IAM policy, `AmazonS3ReadOnlyAccess`, was attached to the EC2 IAM role to provide read-only access to S3.

The project demonstrated S3 access without storing long-term AWS access keys on the EC2 instance.

---

## 🎯 Objective

The objective of this practical was to understand and implement:

* IAM Roles
* IAM Policies
* EC2 Instance Profiles
* Amazon S3 access
* AWS CLI
* AWS STS
* Read-only permissions
* Role-based authentication
* Basic IAM security practices

---

## ☁️ AWS Services Used

* **Amazon EC2**
* **Amazon S3**
* **AWS IAM**
* **AWS STS**
* **AWS CLI**

---

## 🏗️ Architecture

```text
EC2 Instance
     │
     ▼
IAM Role
EC2-S3-ReadOnly-Role
     │
     ▼
AmazonS3ReadOnlyAccess
     │
     ▼
Amazon S3
     │
     ▼
test.txt
```

---

## 🔐 IAM Configuration

### IAM Role

**Role Name:**

`EC2-S3-ReadOnly-Role`

### IAM Policy

**AWS-managed policy:**

`AmazonS3ReadOnlyAccess`

The AWS-managed policy was used instead of creating a custom JSON policy.

This provided read-only access to Amazon S3.

---

## 🛠️ Implementation

### 1. Created an S3 Bucket

A private S3 bucket was created and a test file named `test.txt` was uploaded.

### 2. Created an IAM Role

An IAM role named `EC2-S3-ReadOnly-Role` was created with EC2 as the trusted service.

### 3. Attached the AWS-Managed Policy

The AWS-managed policy:

`AmazonS3ReadOnlyAccess`

was attached to the IAM role.

### 4. Created an EC2 Instance

An Ubuntu EC2 instance was launched for the practical.

### 5. Attached the IAM Role

The `EC2-S3-ReadOnly-Role` was attached to the EC2 instance.

### 6. Verified AWS CLI

The AWS CLI installation and version were verified using:

```bash
aws --version
```

### 7. Verified IAM Identity

The AWS identity being used by the EC2 instance was verified using:

```bash
aws sts get-caller-identity
```

This confirmed that the EC2 instance was using the attached IAM role.

### 8. Listed the S3 Bucket

The S3 bucket was successfully accessed using:

```bash
aws s3 ls s3://YOUR-BUCKET-NAME
```

### 9. Downloaded the S3 Object

The test file was downloaded from S3 using:

```bash
aws s3 cp s3://YOUR-BUCKET-NAME/test.txt .
```

### 10. Verified the File

The downloaded file was verified using:

```bash
cat test.txt
```

### 11. Tested Restricted Access

A write operation was attempted:

```bash
aws s3 cp upload-test.txt s3://YOUR-BUCKET-NAME/
```

The operation was denied because the attached IAM policy provided read-only access.

---

## 🧪 Permission Testing

| Operation            | Result    |
| -------------------- | --------- |
| List S3 bucket       | ✅ Allowed |
| Read/download object | ✅ Allowed |
| Upload object        | ❌ Denied  |
| Delete object        | ❌ Denied  |

---

## 🔒 Security Concept

This project demonstrated role-based access instead of storing long-term AWS access keys on the EC2 instance.

EC2
 ↓
IAM Role
 ↓
IAM Permissions
 ↓
S3


The IAM role allowed the EC2 instance to access S3 according to the permissions provided by the attached policy.

---

## 📚 Key Learnings

* Learned how to create and use IAM Roles.
* Learned how to attach AWS-managed policies to IAM Roles.
* Understood how EC2 uses an IAM Role to access AWS services.
* Practiced AWS CLI commands for S3.
* Used AWS STS to verify the active AWS identity.
* Tested allowed and denied S3 operations.
* Understood the importance of role-based access instead of storing long-term credentials on EC2.
* Practiced read-only permission management.

---

## 📸 Screenshots

1. S3 Bucket

Created a private S3 bucket and uploaded the test object.

Screenshot: 01-s3-bucket.png

2. IAM Role

Created the EC2-S3-ReadOnly-Role for EC2 access.

Screenshot: 02-iam-role.png

3. EC2 as Trusted Entity

Configured EC2 as the trusted entity for the IAM role.

Screenshot: 03-ec2-trusted-entity.png

4. S3 Read-Only Policy

Attached the AWS-managed AmazonS3ReadOnlyAccess policy.

Screenshot: 04-s3-read-only-policy.png

5. IAM Role Attached to EC2

Attached the IAM role to the EC2 instance.

Screenshot: 05-ec2-with-iam-role.png

6. IAM Verification & S3 Access

Verified the IAM identity, listed the S3 bucket, and downloaded the test object.

Screenshot: 06-ec2-s3-access-verification.png

7. Access Denied Test

Verified that write access was denied by the read-only policy.

Screenshot: 07-access-denied.png



## 📌 Project Status

**Completed ✅**

This project successfully demonstrated secure EC2-to-S3 access using an IAM Role and the AWS-managed `AmazonS3ReadOnlyAccess` policy.
