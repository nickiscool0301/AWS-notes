# DynamoDB

## Overview
**NoSQL database** - Fast, flexible, serverless database service  
**Fully managed** - No servers to manage, automatic scaling  
**Single-digit millisecond latency** - High-performance at any scale  
**Global distribution** - Multi-region replication available

## Core Concepts

**Table**
: Collection of data items  
: Schema-free except for primary key  
: Automatically partitions data across multiple servers

**Item**  
: Individual record in table  
: Collection of attributes  
: Maximum size: 400KB per item

**Attribute**  
: Basic data element  
: Name-value pair  
: Scalar, document, or set data types

## Primary Keys

**Partition Key (Simple Primary Key)**
: Single attribute primary key  
: Must be unique across all items  
: Used for data distribution across partitions

**Partition Key + Sort Key (Composite Primary Key)**  
: Two-attribute primary key  
: Partition key groups items, sort key orders within partition  
: Combination must be unique

## Data Types

**Scalar Types**
- **String (S)**: Unicode text
- **Number (N)**: Positive/negative numbers  
- **Binary (B)**: Binary data
- **Boolean (BOOL)**: True or false
- **Null (NULL)**: Unknown or undefined state

**Document Types**
- **List (L)**: Ordered collection of values
- **Map (M)**: Unordered collection of key-value pairs

**Set Types**  
- **String Set (SS)**: Set of strings
- **Number Set (NS)**: Set of numbers
- **Binary Set (BS)**: Set of binary values

## Secondary Indexes

| Index Type | Partition Key | Sort Key | Projection | Use Case |
|------------|---------------|----------|------------|----------|
| **Global Secondary Index (GSI)** | Different from table | Optional, different from table | Configurable | Query different access patterns |
| **Local Secondary Index (LSI)** | Same as table | Different from table | Configurable | Additional sort orders |

**LSI** requires the same partition key as the base table and must be created at table creation time.

**GSI Limits**: 20 per table  
**LSI Limits**: 5 per table (must be created at table creation)

**Projection Options**
: **Keys Only** - Only key attributes  
: **Include** - Keys plus specified attributes  
: **All** - All attributes (highest cost)

## Consistency Models

**Eventually Consistent Reads** (Default)
: May not reflect most recent write operation  
: Lower latency and cost  
: Default for all read operations

**Strongly Consistent Reads**  
: Always return most recent data  
: Higher latency and cost  
: Use `ConsistentRead=true` parameter  
: Not available for GSI queries

## Capacity Modes

| Mode | Scaling | Pricing | Best For |
|------|---------|---------|----------|
| **On-Demand** | Automatic | Pay per request | Unpredictable workloads |
| **Provisioned** | Manual/Auto Scaling | Pay for capacity | Predictable workloads |

**Read Capacity Units (RCU)**
: 1 RCU = 1 strongly consistent read/sec for item up to 4KB  
: 1 RCU = 2 eventually consistent reads/sec for item up to 4KB

**Write Capacity Units (WCU)**  
: 1 WCU = 1 write/sec for item up to 1KB

## DynamoDB Streams

**Purpose**: Capture data modification events in tables  
**Retention**: 24 hours  
**Ordering**: Records appear in same sequence as modifications  
**Integration**: Trigger Lambda functions for real-time processing

**Stream Record Types**
- **KEYS_ONLY**: Only key attributes of modified item
- **NEW_IMAGE**: Entire item after modification
- **OLD_IMAGE**: Entire item before modification  
- **NEW_AND_OLD_IMAGES**: Both new and old images

## Global Tables

**Multi-region replication** - Automatically replicate across regions  
**Multi-active** - Read and write in any region  
**Conflict resolution** - Last writer wins  
**Requirements**: DynamoDB Streams must be enabled

## DAX (DynamoDB Accelerator)

**In-memory cache** - Microsecond latency for DynamoDB  
**Fully managed** - No cache management required  
**Write-through cache** - Consistent with DynamoDB  
**Cluster-based** - Multi-AZ for high availability

## DynamoDB Transactions

**ACID Properties** - Atomic, consistent, isolated, durable operations  
**TransactWriteItems** - Up to 100 write actions across multiple tables  
**TransactReadItems** - Up to 100 read actions with snapshot isolation  
**Additional Cost** - 2x the normal consumed capacity

## Query Operations

**Query**
: Retrieve items with same partition key  
: Can filter by sort key  
: More efficient than Scan  
: Returns sorted results

**Scan**  
: Examine every item in table  
: Can apply filter expressions  
: Less efficient, higher cost  
: Parallel scan available for performance

**Batch Operations**  
: **BatchGetItem** - Retrieve up to 100 items  
: **BatchWriteItem** - Put/delete up to 25 items

## Error Handling

**Exponential Backoff** - Retry with progressively longer delays  
**ProvisionedThroughputExceededException** - Throttling due to capacity limits  
**ConditionalCheckFailedException** - Conditional write failed  
**ValidationException** - Invalid request parameters

## Best Practices
- Design primary key for even data distribution
- Use sort keys for querying patterns
- Avoid hot partitions by distributing access
- Use sparse indexes to reduce costs
- Implement pagination for large result sets
- Use batch operations when possible
- Monitor consumed capacity with CloudWatch
- Use DynamoDB Accelerator (DAX) for read-heavy workloads
- Design for eventually consistent reads when possible