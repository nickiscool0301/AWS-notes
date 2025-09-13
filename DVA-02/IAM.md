# AWS Account root user

- IAM users cannot create CloudFront key pairs -> must log in using root credentials to create ones

# CodeCommit

- Cannot use IAM username and password for CodeCommit

# Billing and Cost Management

- By default, IAM users DO NOT have access to AWS Billing and Cost management
- Need:
    + account admin to grant access to IAM user. 
    + activate IAM user access to the billing and cost management console and attach IAM policy to users
    + then need to activate IAM user access for IAM policies to take effect