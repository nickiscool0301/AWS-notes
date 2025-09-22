# RDS Notes

## Authentication

- You can authenticate to your DB instance using AWS Identity and Access Management (IAM) database authentication
- DB Supported: MySQL, PostgreSQL, and MariaDB

## RDS Proxy
- HA proxy for RDS
- Key points
  - Connection pooling: reuses established connections to DB
  - Scalability: handles thousands of concurrent connections 
  - Failover handling: when failure occurs, proxy redirects connections to healthy DB instances
  - IAM authentication: works with IAM, and Secret Manager
  - Support engines: RDS MySQL, RDS PostgreSQL, Aurora MySQL, Aurora PostgreSQL
- Use cases:
  - Serverless application: Lambda functions can open many connections to RDS, which can exhaust DB connections. RDS Proxy helps manage and pool these connections.
  - Unpredictable workloads: RDS Proxy can handle sudden spikes in traffic by efficiently managing connections.
  - Fast failover and HA    
