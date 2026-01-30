# Day 4 – AWS VPC Deep Dive (Public & Private Subnet Architecture)

## Objective
Design and implement a secure AWS VPC with public and private subnets,
including Internet Gateway and NAT Gateway for controlled internet access.

---

## Architecture Overview
- Custom VPC with CIDR 10.0.0.0/16
- One public subnet and one private subnet
- Internet Gateway for public access
- NAT Gateway for private subnet outbound access

---

## Components Explained

### VPC
A logically isolated virtual network in AWS where resources are launched.

### CIDR Block
- VPC CIDR: 10.0.0.0/16
- Defines private IP range for the VPC

### Public Subnet
- CIDR: 10.0.1.0/24
- Associated with route table pointing to Internet Gateway
- Used for NAT Gateway and public-facing resources

### Private Subnet
- CIDR: 10.0.2.0/24
- No direct route to Internet Gateway
- Uses NAT Gateway for outbound internet access

---

## Step-by-Step Implementation

### 1. Created Custom VPC
- Name: devops-vpc
- CIDR: 10.0.0.0/16

### 2. Created Subnets
- Public Subnet: 10.0.1.0/24
- Private Subnet: 10.0.2.0/24

### 3. Internet Gateway
- Created and attached Internet Gateway to VPC

### 4. Route Tables
**Public Route Table**
- Route: 0.0.0.0/0 → Internet Gateway
- Associated with public subnet

**Private Route Table**
- Route: 0.0.0.0/0 → NAT Gateway
- Associated with private subnet

### 5. NAT Gateway
- Created NAT Gateway in public subnet
- Elastic IP attached

---

## EC2 Testing

### Public Subnet EC2
- Assigned public IP
- Accessible from internet

### Private Subnet EC2
- No public IP
- Internet access via NAT Gateway
- Not accessible from internet

---

## Golden Interview Question

**Q: How does a private subnet access the internet?**

**Answer:**
Private subnet routes outbound traffic to a NAT Gateway in a public subnet,
which then forwards traffic to the Internet Gateway.

---

## IGW vs NAT Gateway

| Feature | Internet Gateway | NAT Gateway |
|------|-----------------|------------|
| Used by | Public subnet | Private subnet |
| Incoming traffic | Allowed | Not allowed |
| Outgoing traffic | Allowed | Allowed |
| Internet exposure | Yes | No |

---

## Key Learnings
- Separation of public and private resources improves security
- NAT Gateway enables safe outbound internet access
- Route tables control traffic flow inside VPC

