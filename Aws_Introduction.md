# IAM

## IAM Policies Structure

The JSON-Structure for IAM policies consists of:
- Version: Policy language version, alwasy include "2012-10-17"
- Id: an identifier for the policy (Optional)
- Statement: one or more indivudal statements (required), which consists of
    - Sid: an identifier for the statement (optional)
    - Effect: Wheter the statement allows or denies access (Allow, Deny)
    - Prinicipal: account/user/role to which this policy applies to
    - Actions: List of actions this policy allows or denies
    - Resource: list of resources to hich the actions applies to
    - Condition: conditions for when this policy is in effect (optional| not reflected in the statement below) 

````json
{
    "Version": "2012-10-17",
    "Id": "S3-Account-Permissions", // Optional
    "Statement": [
        {
            "Sid": "1", //Optional
            "Effect": "Allow",
            "Principial":{
                "Aws":["arn:aws:iam::123456789012:root"]
            },
            "Action":[
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource":["arn:aws:s3:::mybucket/*"]
        }
    ]
}

````

## IAM Security Tools

- IAM Credentials Report (account-level): A report that lists all your account's users and the status of their various credentials
- IAM Access Advisor (user-level): Access advisor shows the service permissions granted to a user and when those services were last accessed. Especially used to revise policies.

## EC2
 
 - EC2 = **Elastic Compute Cloud** which is part of Infrastructure as a Service
 - Capabilities:
    - Renting virtual machines (EC2)
    - Storing data on virtual drives (EBS)
    - Distributing load across machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)

> Be aware that the public IP address always changes on restart of the instance, only the private IP address will remain the same.


### Sizing and Configuration Options:

- Operating Systems: Linux, Microsoft or Mac OS
- Compute Power & Cores (CPU)
- Random-Access memory (RAM)
- Storage Space
    - Network-attached (EBS & EFS)
    - hardware (EC2 Instance Store)
- Network card: Speed of the card, Public IP Address 
- Firewall rules: Security group
- Bootstrap script (configure at first launch): EC2 User Data

### EC2 Script

- It is possible to bootstrap instances using an EC2 User data script
- bootstrapping means launching commands when a machine starts
- The script runs only once at the first start of the instance
- used to automate boot task like:
    - installing updates
    - installing software
    - Downloading common files from the internet
    - Anything you want ...
- it runs with the root user


```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```
### EC2 Instance Types

Naming Conventions:

    m5.2xlarge

- m: instance class
- 5: generation (AWS improves them over time)
- 2xlarge: size within the instance class

Types:

- General Purpose: Balanced VM for diverse workloads (e.g. Web servers)
- Compute Optimized: Compute-intensive tasks with high performance processors (e.g. batch processing workloads)
- Memory Optimized: Fast performance for workloads that process large data sets in memory (e.g. In-memory databases optimized for BI)
- Storage Optimized: For storage-intensive tasks that require high, sequential read and write access to large data sets on local storage (e.g. Relational & NoSQL databases)

[List of Instances and their details][1]

## Security Groups

- Fundamental of network security in AWS
- Control how traffic is allowed into or out of our EC2 instance
- Security groups only contain **allow** rules
- Security groups rules can reference by IP or by security group
- Acting as a "firewall" on EC2 instances
- They regulate:
    - Access to Ports
    - Authorised IP ranges (IPv4 and IPv6)
    - Control of inbound network (from other to the instance)
    - Control of outbound network (from the instance to other)
![SecurityGroups](img/awsCloudPractitioner/securityGroups.png)
  

[1]: https://instances.vantage.sh/