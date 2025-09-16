# Route 53

## Overview
**Scalable DNS service** - Domain name system with high availability  
**Domain registration** - Buy and manage domain names  
**Health checking** - Monitor application health and route traffic  
**Global infrastructure** - Distributed DNS service worldwide

## Core Concepts

**Hosted Zone**
: Container for DNS records for a domain  
: Public hosted zones for internet traffic  
: Private hosted zones for VPC internal traffic

**DNS Records**  
: Instructions for DNS queries  
: Different record types for different purposes  
: TTL (Time-To-Live) controls caching duration

**Name Servers**  
: Servers that respond to DNS queries  
: Route 53 provides 4 name servers per hosted zone  
: Must be configured at domain registrar

## Record Types

| Type | Purpose | Example |
|------|---------|---------|
| **A** | Map domain to IPv4 address | example.com → 192.0.2.1 |
| **AAAA** | Map domain to IPv6 address | example.com → 2001:db8::1 |
| **CNAME** | Alias one domain to another | www.example.com → example.com |
| **MX** | Mail exchange servers | example.com → mail.example.com |
| **TXT** | Text information | Domain verification, SPF records |
| **SRV** | Service discovery | _service._protocol.domain |
| **NS** | Name server records | Delegate subdomain to other servers |
| **PTR** | Reverse DNS lookup | IP address to domain name |

## Alias Records vs CNAME

**Alias Records**
: Route 53 specific extension  
: Can be used for root domain (example.com)  
: Free of charge  
: Only redirect to AWS resources

**CNAME Records**  
: Standard DNS record  
: Cannot be used for root domain  
: Charged per query  
: Can redirect to any domain

**Supported Alias Targets**
- Application Load Balancer
- Network Load Balancer  
- CloudFront distributions
- S3 website endpoints
- API Gateway
- VPC endpoints
- Global Accelerator
- Other Route 53 records in same hosted zone

## Routing Policies

**Simple Routing**
: Single resource for domain  
: No health checks  
: Multiple IP addresses return random selection

**Weighted Routing**  
: Distribute traffic based on assigned weights  
: Useful for A/B testing and gradual deployments  
: Weight 0 stops traffic to resource

**Latency-Based Routing**  
: Route to region with lowest latency  
: Requires latency measurements between users and regions  
: Automatically chooses best performing region

**Failover Routing**  
: Active/passive failover setup  
: Primary resource serves traffic when healthy  
: Secondary resource used when primary fails

**Geolocation Routing**  
: Route based on user's geographic location  
: Country or continent-level routing  
: Default location for unmatched queries

**Geoproximity Routing**  
: Route based on geographic location with bias  
: Bias values shift traffic toward/away from resources  
: Requires Route 53 Traffic Flow

**Multivalue Answer Routing**  
: Return multiple healthy resources  
: Up to 8 healthy records randomly selected  
: Simple load balancing with health checks

## Health Checks

**Types**
- **HTTP/HTTPS**: Check web server health
- **TCP**: Check port connectivity  
- **Calculated**: Combine multiple health checks
- **CloudWatch Alarm**: Based on CloudWatch metrics

**Configuration**
: Check interval: 30 seconds (standard) or 10 seconds (fast)  
: Failure threshold: Number of consecutive failures  
: Success threshold: Number of consecutive successes  
: Global health checkers from multiple regions

**Health Check Locations**
: 15+ global health checking locations  
: Majority must report healthy for overall healthy status  
: Can specify minimum number of health checkers

## Private DNS

**Private Hosted Zones**
: DNS resolution within VPC  
: Not accessible from internet  
: Override public DNS for internal resources

**Requirements**  
: enableDnsHostnames and enableDnsSupport must be true  
: Associate hosted zone with VPC  
: Can associate with multiple VPCs

## Traffic Flow

**Visual Editor**
: Drag-and-drop interface for complex routing  
: Version control for traffic policies  
: Can apply same policy to multiple domains

**Traffic Policy**  
: Reusable configuration for DNS routing  
: JSON-based policy definition  
: Supports all routing policies and health checks

## Resolver

**DNS Resolver**
: Route 53 Resolver provides DNS resolution for VPC  
: Automatically enabled for all VPCs  
: Resolves AWS service names and custom domains

**Resolver Endpoints**  
: Inbound: External DNS servers query VPC resources  
: Outbound: VPC resources query external DNS servers  
: Useful for hybrid cloud DNS resolution

## Best Practices
- Use Alias records for AWS resources when possible
- Implement health checks for critical resources
- Use appropriate TTL values (lower for dynamic content)
- Monitor DNS query patterns with Route 53 query logs
- Use private hosted zones for internal resources
- Implement DNS failover for high availability
- Consider latency-based routing for global applications
- Use weighted routing for gradual deployments