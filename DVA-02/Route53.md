# Comparison of alias and CNAME records

- Alias record only redirect to selected AWS resources (CloudFront, S3 static website hosting, Elastic Beanstalk, API Gateway, VPC endpoint, Global Accelerator), or orther record in the same Route53 hosted zone
- Can create an alias record that has the same name as hosted zone (root domain)

- CNAME record can redirect to any URL, including AWS resources and external domains
- Cannot create a CNAME record that has the same name as hosted zone (root domain).

- Pricing: Alias record is free, CNAME record is charged as standard Route53 queries
