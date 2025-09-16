# CloudFront

## Overview
**Global content delivery network (CDN)** - Deliver content with low latency  
**Edge locations** - 450+ points of presence worldwide  
**Caching** - Reduce load on origin servers  
**Security** - DDoS protection and AWS Shield integration

## Key Concepts

**Distribution**
: Configuration that tells CloudFront where to get content  
: Defines caching behavior and security settings  
: Takes 15-20 minutes to deploy globally

**Origin**  
: Source of content (S3 bucket, HTTP server, Application Load Balancer)  
: Can have multiple origins per distribution  
: Failover support with origin groups

**Edge Location**  
: Global cache servers where content is cached  
: Serves content to users from nearest location  
: Reduces latency and improves performance

## Origins

| Origin Type | Use Case | Features |
|-------------|----------|----------|
| **S3 Bucket** | Static content, websites | Origin Access Control (OAC), versioning support |
| **HTTP/HTTPS** | Dynamic content, APIs | Custom headers, SSL verification |
| **Application Load Balancer** | Auto-scaling applications | Health checks, multiple targets |
| **Media Package** | Live video streaming | Specialized for media content |

## Caching Behavior

**TTL (Time-To-Live)**
: Controls how long objects stay in cache  
: Default TTL: 24 hours  
: Can be overridden by Cache-Control headers

**Cache Key**  
: Determines what makes objects unique in cache  
: Based on URL path by default  
: Can include query strings, headers, cookies

**Cache Policies**  
: Managed policies for common use cases  
: Control what's included in cache key  
: Separate from origin request policies

## Security Features

**Signed URLs and Signed Cookies**
: Control access to private content  
: Time-based or IP-based restrictions  
: Requires CloudFront key pairs (root user only)

**Origin Access Control (OAC)**  
: Secure access to S3 origins  
: Replaces legacy Origin Access Identity (OAI)  
: Uses AWS Signature Version 4 for authentication

**AWS WAF Integration**  
: Web application firewall protection  
: Filter malicious requests at edge  
: Custom rules for application protection

**Field-Level Encryption**  
: Encrypt sensitive data at edge locations  
: Additional layer beyond HTTPS  
: Asymmetric encryption for specific fields

## CloudFront Key Pairs

**Management Restrictions**
: Only AWS account root user can create/manage  
: Cannot use IAM users or roles  
: Maximum 2 active key pairs per account

**Components**
: Public key uploaded to CloudFront  
: Private key used to sign URLs/cookies  
: Associate with trusted signers

**Process**  
1. Root user creates key pair in console
2. Download private key (.pem file)  
3. Upload public key to CloudFront
4. Associate with distribution as trusted signer

## Performance Features

**GZIP Compression**
: Automatic compression for text-based content  
: Reduces transfer time and bandwidth costs  
: Configurable per cache behavior

**HTTP/2 Support**  
: Modern protocol for improved performance  
: Multiplexing and header compression  
: Enabled by default for HTTPS

**Lambda@Edge**  
: Run code closer to users  
: Customize content delivery  
: Four execution points in request/response cycle

## Monitoring & Analytics

**Real-Time Logs**
: Detailed request logs delivered within seconds  
: Kinesis Data Streams integration  
: Customizable fields and sampling rates

**Standard Logs**  
: Detailed access logs  
: Delivered to S3 bucket  
: Contains all request details

**CloudWatch Metrics**
: Request count, data transfer, error rates  
: Geographic and device-based metrics  
: Custom alarms and dashboards

## Distribution Types

**Web Distribution** (Legacy)
: For websites and web applications  
: HTTP and HTTPS content  
: Being replaced by unified distributions

**RTMP Distribution** (Deprecated)  
: For Adobe Flash media streaming  
: No longer recommended  
: Use other streaming solutions

## Price Classes

**Price Class All** - All edge locations (best performance)  
**Price Class 100** - North America and Europe only  
**Price Class 200** - North America, Europe, Asia, Middle East, Africa  

## Best Practices
- Use S3 Transfer Acceleration with CloudFront for global uploads
- Enable compression for text-based content
- Configure appropriate cache behaviors for different content types
- Use Origin Access Control (OAC) instead of OAI for S3 origins
- Monitor performance with Real-Time Logs
- Implement signed URLs for private content access
- Use multiple origins for redundancy and performance
- Consider Regional Edge Caches for large files