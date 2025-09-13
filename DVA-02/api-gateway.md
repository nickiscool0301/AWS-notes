# API Gateway

A fully managed service for creating, publishing, maintaining, monitoring, and securing APIs at any scale.

## Key Concepts & Features

### API Optimization

- **Response Caching:** Caches endpoint responses for a specified TTL (Time-To-Live) to reduce the number of calls made to your backend and improve latency.
- **Payload Compression:** Compresses response payloads to reduce latency and data transfer costs.

### API Endpoint Types

- **Edge-Optimized:** Default. Best for geographically distributed clients. Requests are routed to the nearest CloudFront Point of Presence (POP).
- **Regional:** For clients in the same region as the API.
- **Private:** Can only be accessed from your Amazon VPC using a VPC endpoint.

### Security

- **Authentication & Authorization:**
  - **IAM:** Use AWS IAM roles and policies to authorize access to your APIs.
  - **Cognito User Pools:** Authenticate users through Cognito.
  - **Lambda Authorizers (Custom Authorizers):** Use a Lambda function to perform custom authorization logic.
  - **API Keys:** For tracking and controlling access for specific clients.
- **Throttling & Usage Plans:** Protect your backend from traffic spikes by setting rate limits and quotas.

## Integrations

- **VPC Links:** Connect your API Gateway to private resources within a VPC, like Application Load Balancers or EC2 instances, without exposing them to the public internet.
- **AWS Service Integrations:** Directly integrate with other AWS services (e.g., Lambda, DynamoDB, S3). For example, you can have an API endpoint that directly reads from a DynamoDB table.

## Important Notes

- **ElastiCache:** This is a downstream service. While it can cache data for your backend (e.g., a Lambda function), it does not cache the API Gateway responses themselves. Use API Gateway's built-in caching for that.
- **API Gateway VPC Endpoint:** This allows resources _within_ your VPC to securely access your Private APIs without using an internet gateway.
