# Amazon Cognito

## User Pools vs Identity Pools Comparison

| Feature             | User Pools                                                                                  | Identity Pools                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Primary Purpose     | User directory and authentication                                                           | Temporary AWS credentials and authorization                                                     |
| Main Function       | Manages user sign-up/sign-in                                                                | Provides AWS service access                                                                     |
| Authentication Type | Username/password, social identity, SAML                                                    | Supports anonymous users and authenticated users from various sources                           |
| Output              | JWT tokens (ID, Access, Refresh)                                                            | Temporary AWS credentials (IAM roles)                                                           |
| Common Use Cases    | - Web/mobile app authentication<br>- User profile management<br>- MFA and password policies | - Access AWS services (S3, DynamoDB)<br>- Fine-grained authorization<br>- Anonymous user access |
| Identity Type       | Authentication (Who are you?)                                                               | Authorization (What can you do?)                                                                |
| Best For            | - User management<br>- Social sign-in<br>- Custom auth flows                                | - AWS service access<br>- Role-based access<br>- Guest access                                   |

## Key Points to Remember

- User Pools = Authentication (Identity verification)
- Identity Pools = Authorization (AWS service access)
- They can work together: User Pools can be an identity provider for Identity Pools
- Identity Pools can use other identity providers too (Google, Facebook, etc.)

## Detailed Features

### User Pools

- User directory in Amazon Cognito
- Provides sign-up and sign-in options for your app users
- Features:
  - Built-in customizable UI for sign-in
  - Social sign-in with third party: Facebook, Amazon, Google, Apple
  - MFA, phone/email verification
  - Customizable workflows with AWS Lambda triggers

### Identity Pools

- Create unique identities and federate them with identity providers
- Obtain temporary, limited-privilege AWS credentials
- Supports:
  - Amazon Cognito user pools
  - Open ID Connect (OIDC) providers
  - SAML Identity providers
  - Developer Authenticated identities
- Note: To save user information, identity pools need to be integrated with user pools
