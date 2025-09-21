# SQS (Simple Queue Service)

## Overview

**Fully managed message queuing** - Reliable, scalable message queue service  
**Decouple components** - Separate producers and consumers  
**Two queue types** - Standard and FIFO queues  
**Pay-per-use** - No upfront costs or minimum fees

## Queue Types

| Feature        | Standard Queue         | FIFO Queue                             |
| -------------- | ---------------------- | -------------------------------------- |
| **Delivery**   | At-least-once delivery | Exactly-once processing                |
| **Ordering**   | Best-effort ordering   | Strict FIFO ordering                   |
| **Throughput** | Nearly unlimited       | 300 messages/sec (3,000 with batching) |
| **Duplicates** | Occasional duplicates  | No duplicates                          |
| **Name**       | Any name               | Must end with `.fifo`                  |

## Core Concepts

**Message**
: Data sent between applications  
: Contains body (up to 256KB) and attributes  
: Includes metadata like timestamps and message ID

**Queue**  
: Buffer between message producers and consumers  
: Holds messages until they are processed and deleted  
: Distributed across multiple servers for reliability

**Visibility Timeout**  
: Time message is invisible after being received  
: Prevents other consumers from processing same message  
: Default: 30 seconds, Max: 12 hours

## Message Lifecycle

1. **Producer sends message** to queue
2. **Message stored** redundantly across multiple servers
3. **Consumer receives** message (becomes invisible to others)
4. **Consumer processes** message
5. **Consumer deletes** message from queue
6. **If not deleted**, message becomes visible again after timeout

## Key Features

**Dead Letter Queues (DLQ)**
: Handles messages that can't be processed successfully  
: Configured with main queue, not separate service  
: Helps debug processing issues

**Message Attributes**  
: Metadata attached to messages  
: Name-value pairs with data type  
: Up to 10 attributes per message

**Delay Queues**  
: Postpone delivery of messages  
: 0 seconds to 15 minutes delay  
: Applied to entire queue

**Long Polling vs Short Polling**

| Type              | Wait Time    | API Calls   | Cost        | Use Case                  |
| ----------------- | ------------ | ----------- | ----------- | ------------------------- |
| **Long Polling**  | 1-20 seconds | Fewer calls | Lower cost  | Recommended default       |
| **Short Polling** | 0 seconds    | More calls  | Higher cost | Immediate response needed |

## FIFO Queue Features

Message parameters for FIFO queues:

- MessageGroupId (required)

**Message Groups**
: Messages with same group ID processed in order  
: Different groups can be processed in parallel  
: Group ID required for all FIFO messages

**Deduplication**  
: Prevents duplicate messages within 5-minute window  
: Uses deduplication ID or content-based deduplication  
: Automatic with content-based hashing

## Limits and Quotas

**Message Limits**

- **Size**: 1 byte to 256KB per message
- **Retention**: 1 minute to 14 days (default: 4 days)
- **Receive count**: Track how many times message received
- **In-flight messages**: 120,000 (Standard), 20,000 (FIFO)

**Queue Limits**

- **Name length**: 80 characters maximum
- **Queues per region**: 1 million (soft limit)
- **Message batch size**: 10 messages per batch
- **API rate**: Varies by operation and queue type

## Batch Operations

**SendMessageBatch**
: Send up to 10 messages in single request  
: Reduces API calls and improves throughput  
: Each message can have different attributes

**ReceiveMessage**  
: Retrieve up to 10 messages at once  
: Use `MaxNumberOfMessages` parameter  
: Long polling recommended

**DeleteMessageBatch**  
: Delete up to 10 messages in single request  
: Must provide receipt handles  
: More efficient than individual deletes

## Security Features

**Encryption**
: Server-side encryption with SQS-managed keys (SSE-SQS)  
: AWS KMS encryption (SSE-KMS) for additional control  
: In-transit encryption via HTTPS

**Access Control**  
: IAM policies for user/role-based access  
: SQS resource-based policies  
: Condition keys for fine-grained control

## Error Handling

**Message Visibility**
: Change visibility timeout with `ChangeMessageVisibility`  
: Extend processing time or make immediately visible  
: Handle processing failures gracefully

**Redrive Policy**  
: Automatically move failed messages to DLQ  
: Configure maximum receive count  
: Analyze failures without losing messages

## CloudWatch Integration

**Metrics Available**

- `ApproximateNumberOfMessages`: Messages available
- `ApproximateNumberOfMessagesVisible`: Messages not being processed
- `ApproximateAgeOfOldestMessage`: Age of oldest message
- `NumberOfMessagesSent`: Messages added to queue
- `NumberOfMessagesReceived`: Messages retrieved
- `NumberOfMessagesDeleted`: Messages removed

## Best Practices

- Use long polling to reduce costs and improve efficiency
- Set appropriate visibility timeout based on processing time
- Always delete messages after successful processing
- Use batch operations when processing multiple messages
- Implement dead letter queues for error handling
- Monitor queue depth and message age with CloudWatch
- Use FIFO queues only when strict ordering is required
- Design for idempotent message processing
- Configure appropriate retention periods for your use case

## Note

- To manage large Amazon Simple Queue Service (Amazon SQS) messages, you can use Amazon Simple Storage Service (Amazon S3) and the **Amazon SQS Extended Client** Library for Java. This is especially useful for storing and consuming messages up to 2 GB. Unless your application requires repeatedly creating queues and leaving them inactive or storing large amounts of data in your queues, consider using Amazon S3 for storing your data.
