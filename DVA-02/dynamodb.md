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
