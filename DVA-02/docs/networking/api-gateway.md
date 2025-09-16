# API Gateway

## Overview
**Fully managed API service** - Create, publish, maintain, monitor, and secure APIs  
**Any scale** - Handle thousands of concurrent API calls  
**Multiple protocols** - REST APIs, HTTP APIs, WebSocket APIs  
**Pay-per-use** - No upfront costs or minimum fees

## API Types

| Type | Best For | Features | Cost |
|------|----------|----------|------|
| **REST API** | Full feature set, legacy systems | Caching, request validation, SDK generation | Higher |
| **HTTP API** | Modern applications, lower latency | JWT authorization, CORS | Lower (up to 70% cost reduction) |
| **WebSocket API** | Real-time communication | Bidirectional communication | Pay per message |

## Endpoint Types

**Edge-Optimized** (Default)
: Requests routed to nearest CloudFront edge location  
: Best for geographically distributed clients  
: Uses CloudFront network for optimization

**Regional**  
: For clients in same region as API  
: Lower latency for regional clients  
: Can combine with your own CloudFront distribution

**Private**  
: Accessible only from your VPC  
: Uses VPC endpoints for secure access  
: Not exposed to public internet

## Security & Authorization

**Authentication Methods**
- **AWS IAM**: Use IAM roles and policies
- **Cognito User Pools**: Integrate with Cognito for user authentication  
- **Lambda Authorizers**: Custom authorization logic with Lambda
- **API Keys**: Simple client identification and usage tracking

**Additional Security**
- **Resource policies**: Control access to API resources
- **CORS**: Cross-origin resource sharing configuration
- **Certificate management**: SSL/TLS certificates for custom domains

## Request/Response Features

**Request Validation**
: Validate request parameters and body  
: Reduce backend processing load  
: Return validation errors immediately

**Request Transformation**  
: Modify requests before sending to backend  
: Map parameters and headers  
: Change request format

**Response Transformation**
: Modify responses before returning to client  
: Transform data format  
: Add/remove headers

## Performance & Optimization

**Caching**
: Response caching with configurable TTL (Time-To-Live)  
: Reduces calls to backend services  
: Improves response times and reduces costs

**Throttling**  
: Rate limiting to protect backend services  
: Configurable per-client limits  
: Burst capacity for traffic spikes

**Usage Plans & API Keys**
: Define throttling and quota limits  
: Associate with API keys for tracking  
: Different tiers of service

## Integration Types

**Lambda Integration**
: Direct integration with Lambda functions  
: Synchronous and asynchronous invocation  
: Most common integration pattern

**HTTP Integration**  
: Forward requests to HTTP endpoints  
: Support for HTTP/HTTPS backends  
: Can integrate with ALB, NLB

**AWS Service Integration**  
: Direct integration with AWS services  
: DynamoDB, S3, SNS, SQS without Lambda  
: Reduces latency and complexity

**VPC Link**  
: Connect to private resources in VPC  
: Application Load Balancers and Network Load Balancers  
: Secure communication without internet gateway

## Monitoring & Logging

**CloudWatch Integration**
: API metrics (latency, errors, request count)  
: Custom metrics and alarms  
: Automatic monitoring setup

**Access Logging**  
: Detailed request/response logs  
: Customizable log format  
: Integration with CloudWatch Logs

**AWS X-Ray**  
: Distributed tracing  
: Performance analysis  
: Error detection and debugging

## Limits & Quotas
- **Payload size**: 10MB for REST APIs, 6MB for HTTP APIs
- **Timeout**: 29 seconds maximum
- **Rate limits**: 10,000 requests per second (default)
- **Burst limits**: 5,000 requests (default)
- **API keys**: 500 per account per region

## Best Practices
- Use HTTP APIs for new applications when possible
- Implement proper error handling and status codes
- Enable caching for frequently accessed data
- Use throttling to protect backend services
- Monitor API performance with CloudWatch
- Implement request validation to reduce backend load
- Use least privilege principle for IAM policies