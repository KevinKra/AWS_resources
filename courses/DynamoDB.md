## Introduction

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html

---

### Questions

#### Core Components

- **Explain Tables, Items, and Attributes**
- **Other than primary keys, DynamoDB is schemaless, What does that imply?**
- **What does it mean for an attribute to be scalar?**
- **Items can have nested attributes, how deep of nest does DynamoDB support?**
- **What is a Primary key?**
- **What is a Partition key?**
- **What is a Composite key?**
- **In a table that has only a partition key, can two items can have the same partition key value?**
- **In a table that has a partition key _and_ and sort key, are the items sharing the same partition key stored together?**
- **Must each primary key be scalar?**
- **How does DynamoDB use a partition key's value?**
- **Why is a partition also called a hash attribute, why is a sort key called a range attribute?**
- **Explain how using a composite key provides extra flexibility when querying data.**
- **What are Secondary Indexes?**
- **What are the two types of Indexes that DynamoDB supports?**
- **Explain the Global Secondary Index.**
- **Explain the Local Secondary Index.**
- **What is the default limit of global and local secondary indexes on a given DynamoDB table?**
- **Every index belongs to a table, what is this table called? What would an example of this be?**
- **Does DynamoDB maintain indexes automatically? What does this mean?**
- **When you create an index you must specify what attributes will be copied, or _projected_ from the base table to the index. Explain this concept.**
- **What are the minimum attributes that will be projected from the base table to the index if none are specified?**
- **What are DynamoDB Streams?**
- **Which events trigger a stream record, what data is stored for each type?**
- **How long do stream records last?**
- **Can you use DynamoDB Streams together with AWS Lambda to create triggers? What is an example?**

#### DynamoDB API

- **What is the Control Plane?**
- **What are the five Control Plane Operations?**
- **Describe CreateTable**
- **Describe DescribeTable**
- **Describe ListTables**
- **Describe UpdateTable**
- **Describe DeleteTable**
- **What is the Data Plane?**
- **Explain `PutItem` and `BatchWriteItem`.**
- **Can you use `BatchWriteItem` to delete items from one or more tables?**
- **In what use case is `BatchWriteItem` for efficient than `PutItem`? Why is that?**
- **How many items can be written to a table at once with `BatchWriteItem`?**
- **Explain `GetItem`, `BatchGetItem`, `Query`, and `Scan`.**
- **How many items can be retrieved to a table at once with `BatchGetItem`?**
- **Explain `UpdateItem`.**
- **How does the an atomic counter work in regards to updating items?**
- **Explain `DeleteItem`.**
- **What operation can be used to efficiently batch delete multiple items from tables?**
- **What are the particular CRUD operations of the Data Plane**
- **What do DynamoDB Stream operations let you do?**
- **Describe `ListStreams`, `DescribeStreams`, `GetShardIterator`, and `GetRecords`.**
- **What are Transactions?**
- **Describe `TransactWriteItems` and `TransactGetItems`.**

#### Data Types

- **What are the three data types supported for attributes in tables?**
- **Define Scalar types.**
- **Define Document types.**
- **Define Set types.**
- **What are the five Scalar types?**
- **What are the two Document types?**
- **What is a list, What is a map?**
- **What are Sets?**

#### Read Consistency

- **Can you have tables with the same names in different DynamoDB regions? Would they be considered the same tables, why or why not?**
- **What status code do you get back when your application writes data to a DynamoDB table?**
- **Does DynamoDB support both eventual and strongly consistent reads?**
- **Explain eventual consistency.**
- **Explain strong consistency.**
- **What are four negatives regarding strongly consistent reads?**

#### Read/Write Capacity Mode

- **DynamoDB has two read/write capacity modes for processing reads and writes on your tables. What are they?**
- **Which read/write capacity mode is the default?**
- **Can you set the read/write capacity when creating a table? Can you change this later?**
- **Do global secondary indexes inherit their read/write capacity from the base table?**
- **Briefly describe On-demand mode.**
- **What are read request units and write request units?**
- **What is the expense of read units for strongly consistent read requests and eventually consistent read requests?**
- **What is the atomic data size for read requests, how many units are used per transactions/non-transactions reads?**
- **What is the atomic data size for write requests, how many units are used per transactions/non-transactions writes?**
- **Describe DynamoDB Peak Traffic and Scaling Properties.**
- **What traffic event could result in throttling?**
- **What occurs to the table behavior while switching read/write capacity mode?**
- **Briefly explain Provisioned Mode.**
- **Are the Read and Write Capacity Unit (RCU/WCUs) the same between provisioned and on-demand tables?**
- **Does `DescribeTable` on an on-demand table cost RCU or WCU?**
- **Do you determine the the read and write capacity unit limits of a provisioned table?**
- **Define provisioned throughput.**
- **What status code do you receive when a request is throttled?**
- **Describe DynamoDB autoscaling.**
- **Describe Reserved Capacity.**
- **If you use the AWS Management Console to create a table or global secondary index, is auto scaling enabled by default?**
- **Is reserved capacity available on on-demand mode?**

---

### Answers

- **Explain Tables, Items, and Attributes**

  > DynamoDB tables are broken down into Tables, Items, and Attributes. Similar to other database systems, DynamoDB stores data in tables. A table is a collection of data. Each table contains zero or more items. An item is a group of attributes that is uniquely identifiable among all of the other items. Each item is composed of one or more attributes. An attribute is a fundamental data element, something that does not need to be broken down any further.

- **Other than primary keys, DynamoDB is schemaless, What does that imply?**

  > There is no predefined schema for a table. Other than the primary key, a given table is schemaless, which means that neither the attributes nor their data types need to be defined beforehand. Each item can have its own distinct attributes.

- **What does it mean for an attribute to be scalar?**

  > they can have only one value. Strings and numbers are common examples of scalars.

- **Items can have nested attributes, how deep of nest does DynamoDB support?**

  > DynamoDB supports nested attributes up to 32 levels deep.

- **What is a Primary key?**

  > When you create a table, in addition to the table name, you must specify the primary key of the table. The primary key uniquely identifies each item in the table, so that no two items can have the same key.

- **What is a Partition key?**

  > A simple primary key, composed of one attribute known as the partition key.

- **What is a Composite key?**

  > A Partition Key + a Sort Key. Referred to as a composite primary key, this type of key is composed of two attributes. The first attribute is the partition key, and the second attribute is the sort key.

- **In a table that has only a partition key, can two items can have the same partition key value?**

  > No. Each partition key's value is used by DynamoDB's internal hash function to determine where to physically store (partition) the data in memory.

- **In a table that has a partition key _and_ and sort key, are the items sharing the same partition key stored together?**

  > Yes. The partition key is used in the internal hash function in DynamoDB. The output of the internal hash function determines the partition (physical storage internal to DynamoDB) in which it is stored. All items with the same partition key value are stored together, in sorted order by key value.

- **Must each primary key be scalar?**

  > Each primary key attribute must be a scalar (meaning that it can hold only a single value). The only data types allowed for primary key attributes are string, number, or binary. There are no such restrictions for other, non-key attributes.

- **How does DynamoDB use a partition key's value?**

  > DynamoDB uses the value from the partition key in the internal hash function to determine the physical address in which to store the associated item.

- **Why is a partition also called a hash attribute, why is a sort key called a range attribute?**

  > A partition key is also called a hash attribute because petition keys are used in the internal DynamoDB hashing function that determine the partition in memory for the item.

- **Explain how using a composite key provides extra flexibility when querying data.**

  > Because a composite key consists of both a partition key and a sort key, a composite key allows greater flexibility in querying data.

- **What are Secondary Indexes?**

  > A secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key. DynamoDB doesn't require that you use indexes, but they give your applications more flexibility when querying your data.

- **What are the two types of Indexes that DynamoDB supports?**

  > Global secondary index and Local secondary index.

- **Explain the Global Secondary Index.**

  > Global secondary indexes use neither the partition key or sort key of the base table.

- **Explain the Local Secondary Index.**

  > An index that has the same partition key as the table, but a different sort key.

- **What is the default limit of global and local secondary indexes on a given DynamoDB table?**

  > 20 default global indexes, 5 local indexes.

- **Every index belongs to a table, what is this table called? What would an example of this be?**

  > The table is called a base table. Every index must have a base table. Music table could be a base table, the index (global in this case) could be called GenreAlbumTitle and would at a minimum have the partition and sort keys of the base table as attributes in addition to a unique partition and sort key derived from attributes projected from the base table.

- **Does DynamoDB maintain indexes automatically? What does this mean?**

  > When you add, update, or delete an item on the base table, DynamoDB adds, updates, or deletes the corresponding item in any indexes belonging to that table.

- **What is the term used for copying attributes from a base table into an index?**

  > Projecting!

- **What are the minimum attributes that will be projected from the base table to the index if none are specified?**

  > The partition and sort key from will be, at a minimum, projected into the index.

- **What are DynamoDB Streams?**

  > An optional feature that captures data modification events on DynamoDB tables. The data about these events appear in the stream in near-real time and in the other they occurred.

- **Which events trigger a stream record, what data is stored for each type?**

  > A new item is added to the table: The stream captures an image of the entire item, including all of its attributes.
  > An item is updated: The stream captures the "before" and "after" image of any attributes that were modified in the item.
  > An item is deleted from the table: The stream captures an image of the entire item before it was deleted.

- **How long do stream records last?**

  > 24 hours.

- **Can you use DynamoDB Streams together with AWS Lambda to create triggers? What is an example?**

  > Yes. If you have an employee table and new employees join the company you can trigger lambda functions to send an email (using SES) to the new employee if they have an email attribute.

- **What is the Control Plane?**

  > The lets you create and manage DynamoDB tables, indexes, streams, and other objects dependent on tables.

- **What are the five Control Plane Operations?**

  > CreateTable, DescribeTable, ListTables, UpdateTable, DeleteTable.

- **Describe CreateTable**

  > Creates a new table. Optionally, you can create one or more secondary indexes, and enable DynamoDB Streams for the table.

- **Describe DescribeTable**

  > Returns information about a table, such as its primary key schema, throughput settings, and index information.

- **Describe ListTables**

  > Returns the names of all of your tables in a list.

- **Describe UpdateTable**

  > Modifies the settings of a table or its indexes, creates or removes new indexes on a table, or modifies DynamoDB Streams settings for a table.

- **Describe DeleteTable**

  > Deletes a table.

- **What is the Data Plane?**

  > Data plane operations let you perform create, read, update, and delete (also called CRUD) actions on data in a table. Some of the data plane operations also let you read data from a secondary index.

- **Explain `PutItem` and `BatchWriteItem`.**

  > PutItem and BatchWriteItem are both write actions that add items to the database. BatchWriteItem can write up to 25 items in one call.

- **Can you use `BatchWriteItem` to delete items from one or more tables?**

  > Yes. BatchWriteItem is also the way to delete multiple (up to 25) items from on more tables.

- **In what use case is `BatchWriteItem` more efficient than `PutItem`? Why is that?**

  > BatchWriteItem is suitable for larger write actions. Instead of creating multiple network interactions with PutItems, one BatchWriteItem only requires on network trip.

- **How many items can be written to a table at once with `BatchWriteItem`?**

  > Up to 25 items to a table.

- **Explain `GetItem`, `BatchGetItem`, `Query`, and `Scan`.**

  > GetItem retrieves one item, you can retrieve an entire item or just a subset of attributes. BatchGetItem retrieves up to 100 items from one or more tables. Query retrieves all items that have a specific partition key. You can use a query on a table, provided that the table has both a partition key and a sort key. You can also use a query on an index, provided that the index has both a partition key and a sort key. Scan retrieves all items in the specified table table or index. Optionally, you can apply a filtering condition to return only the values that you are interested in and discard the rest.

- **How many items can be retrieved to a table at once with `BatchGetItem`?**

  > 100

- **Explain `UpdateItem`.**

> UpdateItem – Modifies one or more attributes in an item. You must specify the primary key for the item that you want to modify. You can add new attributes and modify or remove existing attributes. You can also perform conditional updates, so that the update is only successful when a user-defined condition is met. Optionally, you can implement an atomic counter, which increments or decrements a numeric attribute without interfering with other write requests.

- **How does the an atomic counter work in regards to updating items?**

  > Increments or decrements a numeric attribute without interfering with other write requests.

- **Explain `DeleteItem`.**

  > Deletes a single item from a table.

- **What operation can be used to efficiently batch delete multiple items from tables?**

  > BatchWriteItem

- **What are the particular CRUD operations of the Data Plane**

  > All the ones mentioned above.

- **What do DynamoDB Stream operations let you do?**

  > DynamoDB Streams operations let you enable or disable a stream on a table, and allow access to the data modification records contained in a stream.

- **Describe `ListStreams`, `DescribeStreams`, `GetShardIterator`, and `GetRecords`.**

  > ListStreams – Returns a list of all your streams, or just the stream for a specific table.

  > DescribeStream – Returns information about a stream, such as its Amazon Resource Name (ARN) and where your application can begin reading the first few stream records.

  > GetShardIterator – Returns a shard iterator, which is a data structure that your application uses to retrieve the records from the stream.

  > GetRecords – Retrieves one or more stream records, using a given shard iterator.

- **What are Transactions?**

  > Transactions provide atomicity, consistency, isolation, and durability (ACID) enabling you to maintain data correctness in your applications more easily.

- **Describe `TransactWriteItems` and `TransactGetItems`.**

  > TransactWriteItems – A batch operation that allows Put, Update, and Delete operations to multiple items both within and across tables with a guaranteed all-or-nothing result.

  > TransactGetItems – A batch operation that allows Get operations to retrieves multiple items from one or more tables.

- **What are the three data types supported for attributes in tables?**

  > Scalar, Document, and Set types.

- **Define Scalar types.**

  > A scalar type can represent exactly one value. The scalar types are number, string, binary, Boolean, and null.

- **Define Document types.**

  > A document type can represent a complex structure with nested attributes, such as you would find in a JSON document. The document types are list and map.

- **Define Set types.**

  > A set type can represent multiple scalar values. The set types are string set, number set, and binary set.

- **What are the five Scalar types?**

  > Number, String, Binary, Boolean, Null.

- **What are the two Document types?**

  > List (array) and Map (object).

- **What is a list, What is a map?**

  > A List is an array, a Map is an object.

- **What are Sets?**

  > Arrays consisting of one type across all elements.

- **Can you have tables with the same names in different DynamoDB regions? Would they be considered the same tables, why or why not?**

  > You can have tables that have the same name across regions. This is because DynamoDB tables are confined to a region. If two DynamoDB tables share the same name across different regions that is because they **ARE NOT** the same table.

- **What status code do you get back when your application writes data to a DynamoDB table?**

  > 200 status code.

- **Does DynamoDB support both eventual and strongly consistent reads?**

  > Yes. It is eventual by default.

- **Explain eventual consistency.**

  > When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation. The response might include some stale data. If you repeat your read request after a short time, the response should return the latest data.

- **Explain strong consistency.**

  > When you request a strongly consistent read, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful.

- **What are four negatives regarding strongly consistent reads?**

  > A strongly consistent read might not be available if there is a network delay or outage. In this case, DynamoDB may return a server error (HTTP 500). \
  > Strongly consistent reads may have higher latency than eventually consistent reads.
  > Strongly consistent reads are not supported on global secondary indexes.
  > Strongly consistent reads use more throughput capacity than eventually consistent reads.

* **DynamoDB has two read/write capacity modes for processing reads and writes on your tables. What are they?**

  > On-demand and Provisioned (the default).

* **Which read/write capacity mode is the default?**

  > Provisioned.

* **Can you set the read/write capacity when creating a table? Can you change this later?**

  > Yes, this can set both during creation and can also be changed later.

* **Do global secondary indexes inherit their read/write capacity from the base table?**

  > Yes.

* **Briefly describe On-demand mode.**

  > On-demand mode is a flexible billing option capable of serving thousands of requests per second without capacity planning. It offers pay-per-request pricing fpr read and write requests so you only pay for what you use. On-demand mode instantly accommodates your workloads as they ramp up or down to any previously reached traffic level. The request rate is only limited by the DynamoDB throughput default table limits, but it can be raised upon request.

- **What are read request units and write request units?**

  > Units that define the throughput cost for your DynamoDB tables.

- **What is the expense of read units for strongly consistent read requests and eventually consistent read requests?**

  > Strongly consistent reads (transactions) require 2 read units, eventually consistent reads require 1 read unit for an item up to 4KB in size. The number of read requests directly scales up with the size of the item in increments of 4KB.

- **What is the atomic data size for read requests, how many units are used per transactions/non-transactions reads?**

  > 4KB for read requests. 2 RCU for transactions, 1 RCU for non-transactions.

- **What is the atomic data size for write requests, how many units are used per transactions/non-transactions writes?**

  > 1KB for write requests. 2 WCU for transactions, 1 WCU for non-transactions.

- **Describe DynamoDB Peak Traffic and Scaling Properties.**

  > DynamoDB tables using on-demand capacity mode automatically adapt to your application's traffic volume. On-demand capacity instantly accommodates up to double the previous peak traffic for a table. For example: if your traffic pattern varies between 20k to 50k strongly consistent reads per second, on-demand capacity mode instantly accommodates up to 100k reads per second.

- **What traffic event could result in throttling?**

  > if you need more than double your previous peak, DynamoDB automatically allocates more capacity as your traffic volume increases to help ensure your workload does no experience throttling. However, throttling can occur if you exceed double your previous peak within 30 minutes.

- **What occurs to the table behavior while switching read/write capacity mode?**

  > When you switch a table from provisioned capacity mode to on-demand capacity mode, DynamoDB makes several changes to the structure of your table and partitions. This process can take several minutes. During the switching period, your table delivers throughput that is consistent with the previously provisioned write capacity unit and read capacity unit amounts. When switching from on-demand capacity mode back to provisioned capacity mode, your table delivers throughput consistent with the previous peak reached when the table was set to on-demand capacity mode.

- **Briefly explain Provisioned Mode.**

  > If you choose provisioned mode, you specify the number of reads and writes per second that you require for your application. You can use auto scaling to adjust your table’s provisioned capacity automatically in response to traffic changes.

- **Are the Read and Write Capacity Unit (RCU/WCUs) the same between provisioned and on-demand tables?**

  > Yes.

- **Does `DescribeTable` on an on-demand table cost RCU/WCU?**

  > No. It costs 0 RCU/WCU.

- **Do you determine the the read and write capacity unit limits of a provisioned table?**

  > Yes. You can provision the RCU and WCU for a table.

- **Define provisioned throughput.**

  > Provisioned throughput is the maximum amount of capacity that an application can consume from a table or index. If your application exceeds your provisioned throughput capacity on a table or index, it is subject to request throttling.

- **What status code do you receive when a request is throttled?**

  > Throttling prevents your application from consuming too many capacity units. When a request is throttled, it fails with an `HTTP 400` code (Bad Request) and a `ProvisionedThroughputExceededException`. The AWS SDKs have built-in support for retrying throttled requests (see Error Retries and Exponential Backoff), so you do not need to write this logic yourself.

- **Describe DynamoDB autoscaling.**

  > DynamoDB auto scaling actively manages throughput capacity for tables and global secondary indexes. With auto scaling, you define a range (upper and lower limits) for read and write capacity units. You also define a target utilization percentage within that range. DynamoDB auto scaling seeks to maintain your target utilization, even as your application workload increases or decreases.

  > With DynamoDB auto scaling, a table or a global secondary index can increase its provisioned read and write capacity to handle sudden increases in traffic, without request throttling. When the workload decreases, DynamoDB auto scaling can decrease the throughput so that you don't pay for unused provisioned capacity.

- **Describe Reserved Capacity.**

  > With reserved capacity, you pay a one-time upfront fee and commit to a minimum usage level over a period of time. By reserving your read and write capacity units ahead of time, you realize significant cost savings compared to on-demand provisioned throughput settings.

- **If you use the AWS Management Console to create a table or global secondary index, is auto scaling enabled by default?**

  > If you use the AWS Management Console to create a table or a global secondary index, DynamoDB auto scaling is enabled by default.

- **Is reserved capacity available on on-demand mode?**

  > No. Reserved capacity is not available in on-demand mode.

---

### Commands

```
aws dynamodb create-table \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1
```

```
aws dynamodb put-item \
--table-name Music
-- item \
    '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}}' \
--return-consumed-capacity TOTAL
```
