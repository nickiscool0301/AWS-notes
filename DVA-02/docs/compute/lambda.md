# Lambda

## Core Concepts

**Serverless compute** - Run code without managing servers  
**Event-driven** - Triggered by events from AWS services  
**Pay-per-request** - Only pay for compute time used  
**Auto-scaling** - Handles scaling automatically

## Key Limits

- **Memory**: 128MB - 10,240MB (1MB increments)
- **CPU**: Allocated proportionally to memory (can't set directly)
- **Timeout**: 15 minutes max
- **Payload**: 6MB synchronous, 256KB asynchronous
- **Deployment package**: 50MB zipped, 250MB unzipped
- **Concurrent executions**: 1,000 per region (soft limit)

## Concurrency Types

| Type            | Purpose               | Cost             | Auto Scaling |
| --------------- | --------------------- | ---------------- | ------------ |
| **Reserved**    | Limit max concurrency | Free             | No           |
| **Provisioned** | Pre-warm instances    | Pay for capacity | Yes          |

**Reserved Concurrency**
: Sets ceiling for concurrent executions  
: Prevents function from consuming all account capacity  
: Applied to entire function

**Provisioned Concurrency**  
: Pre-initializes instances to eliminate cold starts  
: Applied to specific version/alias  
: Can auto-scale based on schedule/utilization

## Triggers

- **API Gateway**: HTTP requests
- **S3**: Object events
- **DynamoDB**: Stream events
- **SQS/SNS**: Message events
- **CloudWatch Events**: Scheduled events
- **Application Load Balancer**: HTTP requests

## Deployment

- **Deployment package**: ZIP file with code
- **Container images**: Up to 10GB
- **Layers**: Share code/libraries across functions
- **Versions**: Immutable snapshots
- **Aliases**: Mutable pointers to versions

## Environment Variables

- Key-value pairs available to function
- Can be encrypted with KMS
- Useful for configuration without code changes
- Total size: 4KB
- There is no limit to the number of env variables

## Best Practices

- Keep functions small and focused
- Use environment variables for config
- Implement proper error handling
- Monitor with CloudWatch metrics
- Use provisioned concurrency for latency-critical workloads
    - help remove the cold start 
    - keep a fixed number of instance always warm: initialize the exec env before the request comes in

## Good to Know
Moving Lambda from AWS console to AWS CloudFormation:

- Upload all code as a zip to S3, and refer the object in AWS::Lambda::Function block
- Write AWS Lambda code inline in CloudFormation in AWS::Lambda::Function block as long as there are no 3rd-party dependencies
