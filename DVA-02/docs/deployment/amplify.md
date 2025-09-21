# AWS Amplify

AWS Amplify is a **purpose-built platform for static site hosting with Git integration**. It provides a complete solution for deploying and managing modern web applications.

## Key Features

### Git Integration
- Direct integration with Git repositories (GitHub, GitLab, Bitbucket, CodeCommit)
- Automatic deployments triggered by Git commits
- **Provisions environments mapped to branches** for seamless development workflows

### Hosting & Security
- **Provides HTTPS by default** with automatic SSL certificate provisioning
- Global CDN distribution for fast content delivery
- Custom domain support with Route 53 integration

### Serverless Architecture
- **Serverless backend services** including:
  - Authentication (Cognito)
  - APIs (GraphQL/REST via AppSync/API Gateway)
  - Storage (S3, DynamoDB)
  - Functions (Lambda)

### Environment Management
- Branch-based deployments
- Environment variables per branch
- Preview deployments for pull requests
- Atomic deployments with instant rollbacks

## Use Cases
- Single Page Applications (React, Vue, Angular)
- Static site generators (Gatsby, Next.js, Hugo)
- JAMstack applications
- Progressive Web Apps (PWAs)

## Benefits
- Zero-configuration deployments
- Built-in CI/CD pipeline
- Automatic scaling
- Pay-per-use pricing
- Integrated monitoring and analytics