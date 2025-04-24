# AWS CloudFormation Project - Multi-AZ EC2 Deployment with Load Balancer

## Overview

This project demonstrates the deployment of a highly available and scalable web application using AWS CloudFormation. The architecture consists of two EC2 instances placed in different Availability Zones (AZs), each inside its own public subnet. An Application Load Balancer (ALB) is configured to distribute incoming traffic evenly across the instances.

## Architecture

The infrastructure includes:

- **VPC** with public and private subnets in two Availability Zones.
- **Public Subnet 1 (10.0.1.0/24)** in Availability Zone 1
  - EC2 Instance (Server 1)
- **Public Subnet 2 (10.0.3.0/24)** in Availability Zone 2
  - EC2 Instance (Server 2)
- **Private Subnet 1 (10.0.2.0/24)** and **Private Subnet 2 (10.0.4.0/24)** for future use or database tier (not used currently).
- **Internet Gateway** for internet access.
- **Application Load Balancer (ALB)** to distribute traffic to EC2 instances.

## Steps Performed

1. **Created a YAML CloudFormation Template**  
   The template includes resources for:
   - VPC
   - Subnets (public and private)
   - Internet Gateway
   - Route tables and associations
   - EC2 Instances with Apache Web Server installed
   - Security Groups
   - Application Load Balancer with target groups and listeners

2. **Deployed the Template in AWS CloudFormation**  
   Used the AWS Management Console to create a CloudFormation **stack** from the YAML template.

3. **Configured Load Balancer**  
   The ALB was automatically configured to distribute incoming HTTP traffic evenly across the two EC2 instances (Server1 and Server2), hosted in different Availability Zones.

## Outcome

- Each server hosts a different HTML page.
- The ALB successfully routes incoming requests between the two servers to ensure high availability and fault tolerance.

## Benefits

- High availability due to deployment in multiple AZs.
- Load balancing for efficient traffic management.
- Infrastructure as Code (IaC) using YAML for easy replication and versioning.

---

