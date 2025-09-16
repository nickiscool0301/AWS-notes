# Kinesis

## Overview
**Real-time data streaming** - Collect, process, and analyze data in real-time  
**Fully managed** - No infrastructure to manage  
**Scalable** - Handle any amount of streaming data  
**Multiple services** - Different tools for different use cases

## Kinesis Services

| Service | Purpose | Use Case |
|---------|---------|----------|
| **Data Streams** | Real-time data streaming | Custom applications, real-time analytics |
| **Data Firehose** | Data delivery to storage | ETL, data lakes, analytics |
| **Data Analytics** | SQL on streaming data | Real-time dashboards, alerts |
| **Video Streams** | Video streaming | Live video processing, ML analysis |

## Kinesis Data Streams

**Shard**
: Basic unit of capacity  
: 1 MB/sec or 1,000 records/sec input  
: 2 MB/sec output  
: Each record has partition key and sequence number

**Stream**  
: Collection of shards  
: Scales by adding/removing shards  
: Retains data for 1-365 days (default: 24 hours)

**Producer**  
: Sends data records to stream  
: AWS SDK, Kinesis Producer Library (KPL)  
: Partition key determines which shard receives record

**Consumer**  
: Processes data from stream  
: AWS SDK, Kinesis Client Library (KCL)  
: Can be Lambda, EC2, or other applications

## Kinesis Data Firehose

**Purpose**: Deliver streaming data to destinations  
**Destinations**: S3, Redshift, Elasticsearch, Splunk, HTTP endpoints  
**Buffering**: Based on size (1MB-128MB) or time (60-900 seconds)  
**Transformation**: Optional Lambda function for data transformation

**Key Features**
- Automatic scaling
- Data compression and encryption  
- Error record handling
- Data format conversion (JSON to Parquet/ORC)

## Kinesis Data Analytics

**SQL Queries**: Standard SQL on streaming data  
**Sources**: Kinesis Data Streams, Kinesis Data Firehose  
**Destinations**: Kinesis Data Streams, Kinesis Data Firehose, Lambda  
**Windowing**: Tumbling, sliding, and session windows

## Key Concepts

**Partition Key**
: Determines which shard receives record  
: Use high-cardinality keys for even distribution  
: Avoid hot shards with uneven distribution

**Sequence Number**  
: Unique identifier assigned by Kinesis  
: Increases over time within each shard  
: Used for ordering and checkpointing

**Retention Period**  
: How long data is stored in stream  
: 1-365 days (default: 24 hours)  
: Extended retention increases costs

## Scaling

**Resharding**
: Split shards to increase capacity (shard splitting)  
: Merge shards to decrease capacity (shard merging)  
: Manual or automatic scaling

**Enhanced Fan-Out**  
: Dedicated throughput per consumer  
: 2 MB/sec per consumer per shard  
: Lower latency (~70ms vs ~200ms)

## Error Handling

**Put Errors**: Retry with exponential backoff  
**Processing Errors**: Use error records handling  
**Shard Iterator Expiration**: Refresh iterator regularly  
**Throttling**: Increase shards or optimize partition keys

## Integration Patterns

**Lambda Integration**
: Event source mapping triggers Lambda  
: Batch processing of records  
: Automatic retry and error handling

**KCL Applications**  
: Multi-language support (Java, Python, .NET, Node.js)  
: Automatic load balancing across instances  
: Checkpointing for fault tolerance

## Best Practices
- Use high-cardinality partition keys for even distribution
- Monitor shard-level metrics for hot shards
- Implement proper error handling and retries
- Use enhanced fan-out for multiple consumers
- Consider Data Firehose for simple delivery use cases
- Size batches appropriately for better throughput
- Monitor age of oldest record to prevent data loss