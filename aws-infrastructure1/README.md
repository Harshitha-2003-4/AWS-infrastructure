# CloudFormation VPC with Public Subnets, ALB, and EC2 Instances

## Overview
This CloudFormation template provisions a Virtual Private Cloud (VPC) with two public subnets in different Availability Zones (AZs). It deploys two EC2 instances running Apache web servers in the public subnets, serving simple HTML pages. An Application Load Balancer (ALB) is configured to distribute incoming traffic to both EC2 instances.

## Components
- **VPC**: A custom Virtual Private Cloud with CIDR block `10.0.0.0/16`.
- **Public Subnets**: Two public subnets in different AZs (`10.0.1.0/24` and `10.0.3.0/24`).
- **Internet Gateway**: Attached to the VPC for internet access.
- **Route Table**: Configured to route traffic to the internet via the Internet Gateway.
- **EC2 Instances**: Two `t2.micro` EC2 instances in the public subnets.
- **Apache Web Server**: Apache installed on both EC2 instances using UserData script.
- **ALB (Application Load Balancer)**: An internet-facing ALB distributing traffic to both EC2 instances.
- **Security Groups**: Configured to allow HTTP (port 80) traffic.

## How It Works
1. The **ALB** listens for HTTP traffic on port 80 and forwards it to the EC2 instances.
2. The **EC2 Instances** serve simple HTML pages:
   - **Server 1 (Public Subnet 1)**: Displays "You are connected to Server 1".
   - **Server 2 (Public Subnet 2)**: Displays "You are connected to Server 2".
3. Traffic is load-balanced between the two instances, so users will see either "Server 1" or "Server 2" based on the routing.

## Outputs
- **LoadBalancerDNS**: The DNS name of the ALB which can be used to access the application.

## Requirements
- AWS account with appropriate permissions.
- Key pair for EC2 instances (replace the default `vpc-new` with your actual key pair name).
- An AWS region with at least two available Availability Zones.

## Deployment
1. Upload the CloudFormation template to AWS.
2. Launch the stack and provide the required parameters (VPC CIDR, Subnet CIDRs, Instance Type, AMI ID, and Key Name).
3. Once the stack is created, find the **LoadBalancerDNS** in the Outputs section of the CloudFormation stack.
4. Access the ALB DNS URL in a web browser to see the load-balanced response from the EC2 instances.

