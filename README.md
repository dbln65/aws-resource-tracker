# 🧭 AWS Resource Tracker Script

A lightweight Bash script that automates the process of listing AWS resources across multiple services.  
It helps DevOps engineers, cloud administrators, and developers quickly inspect what resources exist in a given AWS account and region using the AWS CLI.

---

## 🚀 Features

This script supports listing resources for the following AWS services:

- **EC2** — Elastic Compute Cloud instances  
- **RDS** — Relational Database Service instances  
- **S3** — S3 buckets  
- **CloudFront** — CDN distributions  
- **VPC** — Virtual Private Clouds  
- **IAM** — Identity and Access Management users  
- **Route53** — Hosted zones  
- **CloudWatch** — Alarms  
- **CloudFormation** — Stacks  
- **Lambda** — Functions  
- **SNS** — Topics  
- **SQS** — Queues  
- **DynamoDB** — Tables  
- **EBS** — Volumes  
- **EKS** — Kubernetes clusters  
- **Cognito** — User pools  
- **ECR** — Container repositories  
- **ACM** — Certificates  

---

## 🧱 Requirements

Before running the script, make sure the following are installed and configured on your system:

1. **Bash** (v4 or higher)  
   Most Linux and macOS systems already include it.  
   On Windows, you can use Git Bash or WSL.

2. **AWS CLI**  
   Install the AWS Command Line Interface:  
   Follow the offical [AWS CLI installation guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
3. **AWS CLI Configuration**
   You must have valid AWS credentials configured:
   ```bash
   aws configure
   ```
   This creates the ~/.aws directory with your credentials and default region.

---

## ⚙️ Usage

  ```bash
   ./aws_resource_list.sh <aws_region> <aws_service>
   ```
Example:
```bash
   ./aws_resource_list.sh eu-central-1 ec2
   ```
This command lists all EC2 instances in the Frankfurt (eu-central-1) region.

Example for a global service:
```bash
   ./aws_resource_list.sh us-east-1 s3
   ```
This lists all S3 buckets (note: S3 is global, not region-specific).

---

## 🧩 How It Works

1. The script checks if:

- AWS CLI is installed

- AWS CLI is configured (~/.aws exists)

2. It reads two command-line arguments:

- aws_region — AWS region (e.g., us-east-1, eu-central-1)

- aws_service — Service name (e.g., ec2, s3, lambda)

3. It uses a case statement to call the appropriate AWS CLI command to list resources.

4. The output is printed directly to the terminal in JSON format (default AWS CLI output).

---

## 🧠 Notes

- Some services (like S3, CloudFront, IAM, and Route53) are global. For those, the region argument is ignored

- You can modify or extend the script easily by adding more AWS services to the case block

- The script does not create, modify, or delete any AWS resources — it is read-only

---

## 🧰 Example Output

```bash
   Listing EC2 instances in eu-central-1
{
    "Reservations": [
        {
            "Instances": [
                {
                    "InstanceId": "i-0123456789abcdef0",
                    "InstanceType": "t3.micro",
                    "State": { "Name": "running" },
                    "Tags": [{ "Key": "Name", "Value": "MyServer" }]
                }
            ]
        }
    ]
}
   ```
