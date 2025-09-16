# IAM (Identity and Access Management)

## Core Components
**Users**: Individual accounts for people or applications  
**Groups**: Collections of users with similar permissions  
**Roles**: Temporary access for users or services  
**Policies**: JSON documents defining permissions

## Policy Types
- **AWS Managed**: Pre-built policies by AWS
- **Customer Managed**: Custom policies you create
- **Inline**: Policies directly attached to users/groups/roles

## Policy Evaluation Logic
1. **Explicit Deny**: Always wins
2. **Explicit Allow**: Required for access
3. **Default**: Implicit deny if no explicit allow

## Authentication Methods
- **Console Password**: Web console access
- **Access Keys**: Programmatic access (CLI/SDK)
- **Multi-Factor Authentication (MFA)**: Additional security layer
- **Temporary Security Credentials**: Short-term access

## Best Practices
- **Least Privilege**: Grant minimum permissions needed
- **Use Groups**: Assign permissions to groups, not users
- **Regular Audits**: Review permissions regularly
- **Strong Passwords**: Enforce password policy
- **Enable MFA**: Especially for privileged users
- **Rotate Keys**: Regular access key rotation

## Root Account
**Use Only For**:
- Account setup and initial configuration
- Creating CloudFront key pairs
- Changing account settings
- Closing account

**Secure Root Account**:
- Enable MFA
- Don't use for daily activities
- Create IAM admin user instead

## Special Cases
**CloudFront Key Pairs**: Only root user can create  
**CodeCommit**: Cannot use IAM username/password, use Git credentials or SSH keys  
**Billing Access**: IAM users need explicit billing permissions + account-level activation

## Cross-Account Access
- **Assume Role**: Temporary access across accounts
- **Cross-Account Policies**: Resource-based policies
- **External ID**: Additional security for role assumption

## Service-Linked Roles
- Pre-defined roles for AWS services
- Created automatically by services
- Cannot be deleted if service is using them
