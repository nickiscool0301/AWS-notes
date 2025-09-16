# Lambda Configuration and Scaling

## CPU Settings

- Lambda does not allow you to set CPU directly
- CPU is allocated based on the amount of memory configured

## Types of Concurrency

| Feature     | Reserved Concurrency           | Provisioned Concurrency                    |
| ----------- | ------------------------------ | ------------------------------------------ |
| Purpose     | Limits maximum concurrency     | Pre-initializes function instances         |
| Use Case    | Limiting resource usage        | Reducing latency for predictable workloads |
| Scaling     | Acts as a ceiling              | Can be auto-scaled                         |
| Application | Entire function (all versions) | Specific versions or aliases               |
| Cost        | No additional cost             | Pay for provisioned instances              |

## Key Points to Remember

- **Reserved Concurrency**:

  - Acts as a hard limit on function concurrency
  - Guarantees maximum number of concurrent executions
  - Cannot be managed by Application Auto Scaling
  - Useful for limiting costs or backend resources

- **Provisioned Concurrency**:
  - Pre-initializes function instances
  - Eliminates cold starts
  - Can be managed by Application Auto Scaling
  - Perfect for predictable workload patterns
  - Can be scheduled (e.g., for sales events)

## Scaling Patterns

1. **Default Scaling**:

   - Functions scale automatically
   - May experience cold starts
   - No additional cost

2. **Reserved Concurrency Pattern**:

   ```
   Function ─► Reserved Concurrency (100)
                └─► Cannot exceed 100 concurrent executions
   ```

3. **Provisioned Concurrency Pattern**:
   ```
   Function ─► Provisioned Concurrency (50)
                └─► Auto Scaling (based on schedule/utilization)
                    └─► Can scale up/down within limits
   ```

## Real-World Example (Black Friday Sale)

```
Before Sale Hours:
└─► Provisioned Concurrency: 10 instances

During Sale (Auto Scaled):
└─► Provisioned Concurrency: Scales to 100 instances
    └─► All requests handled by warm instances
    └─► No cold starts = Consistent low latency
```

## Best Practices

1. Use Provisioned Concurrency when:

   - You have predictable traffic patterns
   - Cold starts are unacceptable
   - You can schedule scaling events

2. Use Reserved Concurrency when:

   - You need to limit resource usage
   - You need to guarantee capacity for specific functions
   - You want to prevent one function from consuming all capacity

3. Monitor and Adjust:
   - Watch ConcurrentExecutions metric
   - Monitor ProvisionedConcurrencySpillover
   - Use Application Auto Scaling for dynamic workloads

## Common Issues

- Cold Starts: Solved by Provisioned Concurrency
- Throttling: Managed by Reserved Concurrency
- Cost Management: Balance between provisioned instances and on-demand scaling
