# EC2 (Elastic Compute Cloud)

## Instance Types
**General Purpose**: T3, T4g, M5, M6i  
**Compute Optimized**: C5, C6i  
**Memory Optimized**: R5, X1e  
**Storage Optimized**: I3, D3  
**Accelerated Computing**: P4, G4

## Tenancy Options
**Shared (Default)**
: Multiple customers share physical hardware

**Dedicated Instance** 
: Hardware dedicated to your account, may share with other instances in same account

**Dedicated Host**
: Physical server completely dedicated to you, bring your own license (BYOL)

## Pricing Models
- **On-Demand**: Pay per hour/second, no commitment
- **Reserved**: 1-3 year commitment, up to 75% savings
- **Spot**: Unused capacity, up to 90% savings, can be interrupted
- **Savings Plans**: Flexible pricing for consistent usage

## Key Features
- **Auto Scaling**: Automatically adjust capacity
- **Load Balancing**: Distribute traffic across instances  
- **Security Groups**: Virtual firewalls
- **Key Pairs**: SSH access (Linux) / RDP access (Windows)
- **User Data**: Bootstrap scripts at launch

## Free Tier
- **t2.micro** or **t3.micro** (1 vCPU, 1GB RAM)
- **750 hours/month** for first 12 months
- Linux/Windows eligible
