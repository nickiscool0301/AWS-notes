# EC2 (Elastic Compute Cloud)

## Instance Types

**General Purpose**: T3, T4g, M5, M6i  
**Compute Optimized**: C5, C6i  
**Memory Optimized**: R5, X1e  
**Storage Optimized**: I3, D3  
**Accelerated Computing**: P4, G4

## Tenancy Options

**Shared (Default)**
: Multiple customers share physical hardware

**Dedicated Instance**
: Hardware dedicated to your account, may share with other instances in same account

**Dedicated Host**
: Physical server completely dedicated to you, bring your own license (BYOL)

## Pricing Models

- **On-Demand**: Pay per hour/second, no commitment
- **Reserved**: 1-3 year commitment, up to 75% savings
- **Spot**: Unused capacity, up to 90% savings, can be interrupted
- **Savings Plans**: Flexible pricing for consistent usage

## Key Features

- **Auto Scaling**: Automatically adjust capacity
- **Load Balancing**: Distribute traffic across instances
- **Security Groups**: Virtual firewalls
- **Key Pairs**: SSH access (Linux) / RDP access (Windows)
- **User Data**: Bootstrap scripts at launch

## Free Tier

- **t2.micro** or **t3.micro** (1 vCPU, 1GB RAM)
- **750 hours/month** for first 12 months
- Linux/Windows eligible

## Query metadata for instance

- Query the metadata at http://169.254.169.254/latest/meta-data

## Use case notes

1. Bussiness application is hosted on EC2 isntances. The business has requested a solution to track average response time, and send a notification to the admin if it exceeds a threadhold
   -> Can use CloudWatch and SNS

- Configure application write the response time to a log file.
- Install and config CloudWatch agent on the EC2 instances to monitor the log file and send the data to CloudWatch Logs
- Create a CloudWatch alarm to send an Amazon Simple Notification Service (Amazon SNS) notification when the average of the response time metric exceeds the threshold

2. How to disable the attribute 'DeleteOnTermination' for root EBS volume while the EC2 is running
   -> AWS Console does not allow -> can use AWS CLI or SDK
