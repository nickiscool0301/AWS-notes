# Primary key

- must specify primary key when creating a table
- Two types:
  - partition key: simple primary key, single attribute
  - partition key and sort key: composite primary key, two attributes.

# Secondary indexes

- enable to query the data in the table using an alternate key, different from the primary key
- Two types:
  - Global secondary index: an index with a partition key and a sort key that can be different from those on the table
  - Local secondary index: an index that has the same partition key as the table, but a different sort key.

Quota: 20 global secondary indexes and 5 local secondary indexes per table.

# Consistency models

- DynamoDB supports eventually consistent and strongly consistent reads:
  - Eventually consistent reads (DEFAULT):
    - response not reflect of the recently completely write operations
    - stale data might be returned
  - Strongly consistent reads:
    - always reflect all writes that received a successful response prior to the read
    - higher latency and more expensive
    - apply ConsistentRead parameter and set it to true for GetItem, Query, Scan operations.
