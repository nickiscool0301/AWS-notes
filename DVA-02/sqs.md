# SQS

## Key Points to Remember

- Two types of queues:
  - Standard Queue: At-least-once delivery, best-effort ordering
  - FIFO Queue: Exactly-once processing, strict ordering
- Default retention period: 4 days (Configurable from 1 minute to 14 days)
- Maximum message size: 256KB
- Long polling vs Short polling:
  - Long polling (1-20 seconds): Reduces API calls, recommended for cost savings
  - Short polling (0 seconds): Immediate response, more API calls
- Visibility Timeout:
  - Default: 30 seconds
  - Min: 0 seconds
  - Max: 12 hours
  - Can be changed using ChangeMessageVisibility API

## Message Lifecycle

1. Producer sends message
2. Message is redundantly distributed
3. Consumer receives message (becomes invisible to other consumers)
4. Message is processed
5. Message is deleted by consumer
6. If not deleted before visibility timeout, message becomes visible again

## Important Quotas & Limits

- In-flight messages (messages being processed):
  - Standard queue: 120,000 messages per queue
  - FIFO queue: 20,000 messages per queue
- Message retention: 1 minute to 14 days (default: 4 days)
- Delay queue: 0 seconds to 15 minutes
- Message size: 1 byte to 256KB
- Queue name: 80 characters maximum
- Maximum receives per message: 1,000 messages per API call
- FIFO Queue specific:
  - Maximum throughput: 300 messages/second (with batching)
  - 3,000 messages per second with batching using multiple message group IDs
  - Messages must have a Message Group ID
  - Deduplication ID required (either provided or content-based)
  - Queue name must end with .fifo suffix

## Best Practices

- Use Long Polling when possible (reduces costs)
- Set appropriate visibility timeout based on processing time
- Always delete messages after successful processing
- Use batch operations when possible (SendMessageBatch, DeleteMessageBatch)
- For ordered messages, use FIFO queues
- Monitor CloudWatch metrics:
  - ApproximateNumberOfMessagesVisible
  - ApproximateAgeOfOldestMessage
  - ApproximateNumberOfMessagesNotVisible
