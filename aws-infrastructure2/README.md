# AWS CloudFormation: Private S3 Access via VPC Gateway Endpoint

This project sets up an AWS architecture that allows an EC2 instance to access an S3 bucket **privately** using a **VPC Gateway Endpoint**, without requiring internet access.

## Architecture Overview

The CloudFormation stack provisions the following AWS resources:

- **VPC** with CIDR block `10.0.0.0/16`
- **Public Subnet** `10.0.0.0/24`
- **Internet Gateway** attached to the VPC
- **Route Table** with a route `0.0.0.0/0` to the Internet Gateway
- **EC2 Instance** (Ubuntu) in the public subnet
- **Security Group** for EC2 (allows **SSH (22)** and **HTTP (80)**)
- **VPC Gateway Endpoint** for S3
- **Security Group** for VPC Endpoint
- **S3 Bucket** with a **bucket policy** that allows access only via the VPC Endpoint

##  Security Rules

- **EC2 Security Group**:
  - Inbound: SSH (22) and HTTP (80) from anywhere (`0.0.0.0/0`)
  - Outbound: All traffic

- **S3 Access**:
  - Only allowed from the EC2 instance via the **VPC Gateway Endpoint**
  - Denies all public internet access to the S3 bucket

##  EC2 Instance

- EC2 instance is launched in the **public subnet**
- It installs Apache (Ubuntu: `apache2`) and serves a simple HTML page
- The instance can access the S3 bucket **privately**, using the gateway endpoint — not the public internet

## S3 Bucket Policy

The S3 bucket policy is configured to:

- Allow access **only from the VPC Endpoint**
- Deny access from outside of the VPC

## Deployment Notes

Once the stack is deployed, you will have a fully working infrastructure where:

- The EC2 instance is publicly reachable for SSH/HTTP
- S3 access is restricted to private VPC traffic only through the VPC endpoint

This setup is ideal for securing access to S3 while still allowing necessary public access to your application.
