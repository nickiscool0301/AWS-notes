# Elastic Beanstalk Deployment Policies Comparison

| Feature                     | All at Once                            | Rolling                                | Rolling with Additional Batch          | Immutable                                 | Blue/Green                           |
| --------------------------- | -------------------------------------- | -------------------------------------- | -------------------------------------- | ----------------------------------------- | ------------------------------------ |
| Deploy Time                 | Fastest ⚡️                            | Moderate 🕒                            | Slow 🕒                                | Slower 🕒                                 | Slowest ⏰                           |
| Zero Downtime?              | ❌ Has downtime                        | ✅ Minimal impact                      | ✅ No downtime                         | ✅ No downtime                            | ✅ No downtime                       |
| Impact of Failed Deployment | High Risk ⚠️<br>All instances affected | Medium Risk 🔶<br>Only subset affected | Low Risk ✅<br>Only subset affected    | Very Low Risk ✅<br>No impact on existing | Very Low Risk ✅<br>Easy rollback    |
| Rollback Process            | Manual redeploy<br>Slow & complex      | Manual redeploy<br>Rolling back        | Manual redeploy<br>Rolling back        | Quick ⚡️<br>Terminate new instances      | Instant ⚡️<br>Switch to old version |
| Code Deployed to            | Existing instances                     | Existing instances<br>in batches       | Existing + new instances<br>in batches | New instances only                        | New environment                      |
| DNS Change                  | No                                     | No                                     | No                                     | No                                        | Yes                                  |

## Key Characteristics

### All at Once

- Deploys to all instances simultaneously
- Fastest but highest risk
- Best for dev/test environments
- Has downtime during deployment

### Rolling

- Updates instances in batches
- Reduced capacity during deployment
- Some instances serve old version while others new
- Good for production with acceptable partial degradation

### Rolling with Additional Batch

- Like rolling but launches new instances first
- Maintains full capacity
- Takes longer but safer
- Good for production requiring full capacity

### Immutable

- Launches new instances with new version
- Zero downtime and quick rollback
- More expensive (double capacity temporarily)
- Safest for production

### Blue/Green

- Creates entirely new environment
- Zero downtime and instant rollback
- Most expensive (double capacity until swap)
- Best for critical production applications
- Requires DNS change (Route 53)

## Best Practices

- Dev/Test: Use All at Once for speed
- Production (cost-sensitive): Use Rolling with Additional Batch
- Production (critical): Use Immutable or Blue/Green
- Always test deployment policy in dev/test environment first
