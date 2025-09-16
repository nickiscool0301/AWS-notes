# Elastic Beanstalk

## Overview
**PaaS (Platform as a Service)** - Deploy applications without managing infrastructure  
**Supported Languages**: Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker  
**Handles**: Load balancing, auto-scaling, monitoring, patching

## Deployment Policies

| Policy | Downtime | Risk | Speed | Best For |
|--------|----------|------|-------|----------|
| **All at Once** | Yes | High | Fastest | Dev/Test |
| **Rolling** | No | Medium | Moderate | Production |
| **Rolling + Batch** | No | Low | Slow | Production (maintain capacity) |
| **Immutable** | No | Very Low | Slower | Critical production |
| **Blue/Green** | No | Very Low | Slowest | Mission-critical |

**All at Once**
: Deploy to all instances simultaneously  
: Has downtime, fastest deployment

**Rolling**  
: Deploy in batches, reduced capacity during deployment  
: No downtime, some instances serve old version

**Rolling with Additional Batch**  
: Launch new instances first, then deploy in batches  
: Maintains full capacity, longer deployment time

**Immutable**  
: Launch new instances with new version  
: Zero downtime, quick rollback, higher cost

**Blue/Green**  
: Create new environment, swap URLs  
: Zero downtime, instant rollback, requires Route 53

## Components
- **Application**: Collection of components (environments, versions)
- **Application Version**: Deployable code
- **Environment**: Running application version
- **Configuration Template**: Environment settings template

## Key Features
- **Auto Scaling**: Automatically adjust capacity
- **Load Balancer**: Distribute traffic
- **Health Monitoring**: Application and instance health
- **Version Management**: Track application versions
- **Log Collection**: Centralized logging

## Configuration
- **.ebextensions**: YAML/JSON files in source code
- **Environment Variables**: Runtime configuration
- **Configuration Files**: Infrastructure settings
- **Saved Configurations**: Reusable environment templates

## Supported Platforms
- **Web Servers**: Apache, Nginx, IIS
- **Application Servers**: Tomcat, Passenger, Puma
- **Docker**: Single/multi-container
