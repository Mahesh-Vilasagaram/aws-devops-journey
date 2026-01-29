# Day 3 – AWS IAM Deep Dive & Role-Based Access

## Objective
Understand and implement IAM roles for EC2 without using access keys.

---

## IAM Concepts
- **IAM User**: Human access to AWS
- **IAM Role**: Temporary permissions for AWS services
- **IAM Policy**: JSON document defining permissions

**Golden Rule**: Users log in, roles are assumed.

---

## Lab Performed

### 1. Created IAM Role
- Role Name: EC2-S3-ReadOnly-Role
- Trusted Entity: EC2
- Permissions: AmazonS3ReadOnlyAccess

### 2. Attached Role to EC2
- EC2 instance assigned IAM role
- No access keys used

### 3. Tested Role Access (from EC2)
```bash
aws s3 ls

