# Cognito

## Core Concepts
**User management and authentication** - Secure user directory and identity broker  
**Two main components** - User Pools (authentication) and Identity Pools (authorization)  
**Federated identity** - Support for social and enterprise identity providers  
**JWT tokens** - Secure token-based authentication

## User Pools vs Identity Pools

| Feature | User Pools | Identity Pools |
|---------|-----------|----------------|
| **Purpose** | Authentication (Who are you?) | Authorization (What can you do?) |
| **Function** | User directory and sign-in | AWS service access via IAM roles |
| **Output** | JWT tokens (ID, Access, Refresh) | Temporary AWS credentials |
| **Users** | Registered users only | Supports anonymous and authenticated |
| **Identity Sources** | Username/password, social, SAML | Multiple providers including User Pools |

## User Pools Features

**Authentication Methods**
: Username/password with customizable password policies  
: Social sign-in (Facebook, Google, Amazon, Apple)  
: SAML and OpenID Connect providers  
: Multi-factor authentication (SMS, TOTP)

**Security Features**  
: Advanced security with risk-based authentication  
: Account takeover protection  
: Compromised credentials detection  
: Device tracking and management

**Customization**
: Lambda triggers for custom workflows  
: Customizable UI for hosted sign-in pages  
: Custom attributes and verification methods

## Identity Pools Features

**Identity Sources**
: Cognito User Pools  
: Social identity providers (Facebook, Google, etc.)  
: SAML providers  
: OpenID Connect providers  
: Developer authenticated identities  
: Anonymous (guest) users

**AWS Integration**
: Temporary AWS credentials via STS  
: Fine-grained IAM policies based on identity  
: Support for authenticated and unauthenticated roles

## JWT Tokens (User Pools)

**ID Token**
: Contains user identity information  
: Used for authentication verification  
: Expires after 1 hour (default)

**Access Token**  
: Used to access User Pool resources  
: Contains scopes and groups  
: Expires after 1 hour (default)

**Refresh Token**  
: Used to obtain new ID and Access tokens  
: Longer expiration (30 days default, up to 10 years)

## Common Integration Patterns

**Web/Mobile App Authentication**
1. User signs in through User Pool
2. Receive JWT tokens
3. Use tokens to authenticate API calls

**AWS Service Access**  
1. User authenticates with User Pool
2. Exchange JWT for AWS credentials via Identity Pool
3. Use credentials to access AWS services (S3, DynamoDB, etc.)

**Anonymous Access**
1. Get temporary credentials from Identity Pool
2. Access limited AWS resources as guest user

## Best Practices
- Use User Pools for user management and authentication
- Use Identity Pools for AWS service access
- Enable MFA for sensitive applications
- Implement proper token refresh logic
- Use least privilege IAM policies for Identity Pool roles
- Monitor authentication events with CloudWatch