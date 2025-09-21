# X-Ray

# X-Ray with AWS Fargate

## Setup

- Provide IAM task role to X-Ray container
- Deploy X-Ray daemon as sidecar container

# SDK

AWS_XRAY_DAEMON_ADDRESS

- Set the host and port of the X-Ray daemon listener.
- By default, the SDK uses 127.0.0.1:2000 for both trace data (UDP) and sampling (TCP).
- Use this variable if you have configured the daemon to listen on a different port or if it is running on a different host

## Sampling

- Sampling rules determine which requests to trace
- Default rule: 1 request per second, 5% of additional requests
- Custom rules can be created and prioritized
- Sampling can be disabled in SDK configuration

## Indexing

- Indexes are created for trace data to enable searching
- Instrumentation: **annotation**
