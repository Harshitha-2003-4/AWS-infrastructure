# AWS Infrastructure: VPC Endpoint Access to S3 via EC2

This project provisions AWS infrastructure using CloudFormation to securely access an S3 bucket from an EC2 instance without using the public internet.

##  Resources Created

- **VPC**: 10.0.0.0/16
- **Public Subnet**: 10.0.0.0/24
- **Internet Gateway**: Attached to the VPC for outbound internet access
- **Route Table**: Routes 0.0.0.0/0 traffic to the Internet Gateway
- **EC2 Instance**: Deployed in the public subnet
- **EC2 Security Group**: Allows SSH (port 22) and HTTP (port 80)
- **VPC Gateway Endpoint**: Configured for Amazon S3
- **VPC Endpoint Security Group**: Controls access to the S3 bucket from the EC2 instance
- **S3 Bucket**: Configured with a bucket policy to allow access **only via the VPC Endpoint**

##  Outcome

- **Access to S3**: The EC2 instance can successfully access the S3 bucket through the VPC Gateway Endpoint **without needing internet access**.
- **Security**: The S3 bucket is not publicly accessible and only responds to requests routed through the configured VPC Endpoint, ensuring secure and private connectivity between EC2 and S3.

##  Steps to Test Access

1. **SSH into EC2 Instance**:
   - Once the CloudFormation stack is deployed, SSH into the EC2 instance using its public IP:

2. **Test S3 Access**:
   - Ensure that the AWS CLI is installed on the EC2 instance, then test access to the S3 bucket:
   
     bash
     aws s3 ls s3://<your-bucket-name>

   - This should list the contents of the S3 bucket, confirming that the EC2 instance can access the S3 bucket through the VPC endpoint.

3. **Verify No Public Internet Access**:
   - To confirm that access is only available via the VPC endpoint, try accessing the S3 bucket using a public method, such as `curl` or `wget`. These requests should fail if the VPC endpoint is functioning correctly.
   
     bash
     curl https://<your-bucket-name>.s3.amazonaws.com
     
     If configured properly, the EC2 instance should not be able to access the bucket through the public internet.

## CloudFormation Template

This setup uses an AWS CloudFormation YAML template to deploy all the resources described above. Ensure that the VPC endpoint is configured for S3 to enforce private access to the bucket.
