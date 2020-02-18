## IAM 101 -- Identity Access Management

> IAM allows you to manage users, groups, and roles and their corresponding level of access to the AWS Platform.

### IAM Permission Entities

- **Users**
  - The atomic unit for permissions. User can be assigned permissions uniquely or across more broad setups like groups.
- **Groups**
  - Share traits amongst users.
  - EX: SysAdmins are all part of one group, Marketing team is part of another, etc.
- **Roles**
  - Can be used to delegate access to AWS resources, users, groups, and services.
  - EX: EC2 instance can have read/write access to S3 bucket.
- **Policies (Policy Documents)**
  - Policies that are written and applied to roles, users, and groups.
  - Can be (and usually is, if not always) written in JSON.

### Role Security

- **Prompt**: You have provisioned an EC2 instance and you want it to have access to S3. How should this be done?
- **Wrong**: Create a new IAM user and grant read access to S3. Store the user's credentials locally on the EC2 instance and configure your application to supply the credentials with each API request. It is a dangerous security practice to store credentials on the instance istelf, if it is compromised so is the s3 bucket.
- **Correct**: Create an IAM role with read-access to S3 and assign the role to the EC2 instance

### Review

- IAM is universal, it is global.
- Root account is the account created when AWS account is made. For day-to-day access _do not_ use root account, make User with appropriate permissions.
- No users have _No permissions_ when first created.
- New users are assigned an **Access Key ID & Secret Access Keys** when first created. These keys are not the same as a password, though they can be used through APIs and the CLI.
- You can only view and download the Access Keys once, if you lose access to the _secret access key_ it must be regenerated. Save these in a secure location.
- You can create and rotate your own password rotation policies.

#### Questions

- Which IAM entity can you use to delegate access to your AWS resources to users, groups or services?
- Does AWS recommend that EC2 instances have credentials stored on them so that the instances can access other resources (such as S3 buckets)? Why not?
- What is an IAM Policy?
- What is an IAM User?
- What is an IAM Role?
- What is an IAM Group?

---

## EC2 -- Elastic Compute Cloud

> A web service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain server instances to minutes, allowing you to quickly scale capacity both up and down as requirements change.

### Pricing Options

- **On Demand**
  - Allows you to pay a fixed rate by the hour (or by the second) with no commitment.
- **Reserved**
  - Provides you with a capacity reservation and offers a significant discount on the hourly charge.
  - 1 to 3 year terms.
- **Spot**
  - Enables you to bid whatever price you want for instance capacity.
  - Provides greater savings if your applications have flexible start and end times.
  - If AWS Terminates EC2 instance, you aren't charged for hour. If you cancel, you are charged for full-hour.
- **Dedicated Host**
  - Physical EC2 host dedicated for your use.
  - Dedicated Hosts reduce costs by allowing you to use your existing server-bound software licenses.
  - Suitable for advanced server license requirements, ie medical or PII bound data stores.

### Use Cases

- **On Demand Instance**
  - Suitable for users that want low-cost of flexibility of AWS without an upfront payment or contract commitment.
  - Applications with short term, spiky, or unpredictable workloads that cannot be interrupted.
  - Applications being developed or tested on Amazon EC2 for the first time.
- **Reserved Instance**
  - Applications with steady state / predictable usage.
  - Users can make upfront payments to reduce the cost even further.
  - All upfront with maximum contract will result in most savings.
  - Standard RI (up to 75% off on-demand)
  - **Convertible RI** (up to 45% off on-demand) have the capability to change the attributes of the RI as long as the exchange results in the creation of RI of equal or greater value.
  - **Scheduled RIs** are able to launch within the window you reserve. This option allows you to match your capacity to a predictable recurring schedule. EX: End of week sales expect extra traffic.
- **Spot Instance**
  - Flexible start and end times.
  - Feasible at very low compute prices.
  - Often used for cheap massive volume or when budgets are extremely limited for compute.
- **Dedicated Host**
  - Used to regulatory requirements that do not support to multi-tenant virtualization.
  - Great for licensing which does not support multi-tenancy or cloud deployments.
  - Can be purchased On-Demand (hourly) or as a Reservation.

### EC2 Instance Types

> NOTE: There are more instance types since these notes were taken

- **F1** - Field Programmable Gate Array
  > Financial Analytics, Big-data, real-time video processing.
- **I3** - High Speed Storage
  > NoSQL DBs, Data warehousing.
- **G3** - Graphics Intensive
  > Video Encoding, 3D App streaming
- **H1** - High Disk Throughput
  > Distributed file systems
- **T2** - Lowest cost, general purpose
  > Web servers, small DBs
- **D2** - Dense Storage
  > Fileservers, Data warehousing
- **R4** - Memory Optimized
  > Memory Intensive Apps/DBs
- **M5** - General Purpose
  > Application Servers
- **C5** - Compute Optimized
  > CPU Intensive Apps/DBs
- **P3** - Graphics/Gen Purpose GPU
  > Machine Learning, BitCoin mining, etc.
- **X1** - Memory Optimized
  > SAP HANA, Apache Spark, etc.

### EBS -- Elastic Block Storage

- Allows you to create storage volumes (discs) and attach them to EC2 instances. Thing SSD / HDD attached to a CPU.
- Once attached, you can create a file system on top of the volume, use them anyway you would use a block device.
- EBS volumes are placed in specific AZ where they are _automatically replicated_ to protect you from component failure.
- **Root Device** - EBS disc that OS is installed onto (aka boot volume / :C// Drive ).

### EBS Volume Types

#### SSD

- **General Purpose SSD (GP2)**
  - Below 10,000 IOPS
  - Balance of price and performance
- **Provisioned IOPS SSD (IO1)**
  - Over 10,000 IOPS
  - Highest-performance SSD

#### Magnetic (HDD)

- **Throughput Optimized HDD (ST1)**
  - Not bootable
- **Cold HDD (SC1)**
  - Not bootable
- **Magnetic (Standard)**
  - Legacy
  - Only bootable HDD

### Review

- If a spot instance is terminated by Amazon EC2 you will not be charged for a partial hour of usage. If you terminate the instance, you will be charged for the complete hour the instance ran.

#### Questions

- What are the four EC2 pricing options?
- What are the reserved instance contract lengths?
- Explain the features and use case of each EC2 pricing option.
- What are the EC2 Instance Types?
- What is Elastic Block Storage?
- What are the EBS Volume Types?
- Which magnetic discs are bootable?

---

## S3 -- Simple Storage Service

> Provides developers and IT teams with secure, durable, highly-scalable object storage.

### Overview

- S3 is Object-based - i.e. allows you to upload files
- Files can be 0 to 5 TB
- Unlimited Storage
- Files are stored in Buckets (folders)
- S3 is a universal namespace
- When you upload a file to S3 you will receive a 200 message if you're using an API or CLI

### Data Consistency Model

- **POST** - Immediate Read after write consistency
- **PUT / DELETE** - Eventual consistency

### Storage Structure

- S3 is a Simple Key-Value store.
  > Key + Value, VersionID, MetaData, Sub-resources
- Sub-resources - bucket-specific configuration
  - Bucket Policies
  - Access Control Lists
  - Cross Origin Resource Sharing (CORS)
  - Transfer Acceleration

### S3 Basics

- Built for 99.99% uptime
- Amazon guarantee 99.9% availability
- Amazon guarantees 99.999999999% (11-9s) durability
- Tiered Storage Available
- Life-cycle Management
- Versioning
- Encryption
- Secure Data access
  - Control Lists
  - Bucket Policies

### S3 Storage Tiers/Classes

> S3, S3-IA, S3-IA One Zone, S3-Intelligent Tiering, S3-Glacier, S3-Glacier Deep Archive

- **S3**

  - 99.99% Available, 9x11% Durability
  - Stored redundantly in multiple devices in multiple facilities
  - Designed to sustain the loss of 2 facilities concurrently

- **S3-IA (Infrequently Accessed)**

  - Same as S3 standard, but...
  - For data that is used less frequently, but requires rapid access when needed
  - Lower fee than S3, but charged a retrieval fee

* **S3 One Zone-IA**

  - Same as IA, but data is stored in a single AZ
  - Same durability, 995% availability
  - 20% Cheaper than S3-IA

* **S3-Intelligent Tiering**

  - Unknown or unpredictable access patterns
  - 2 tiers - frequent and infrequent access
  - Automatically moves your data to most cost-effective tier based on how frequently you access each object

* **S3 Glacier**

  - Low-cost design is ideal for long-term archive
  - Takes between 3-5 hours to retrieve data from Glacier
  - Configurable retrieval times, from minutes to hours

* **S3 Glacier Deep Archive**
* Lowest cost storage class designed for long-term retention of data that will be retained for 7-10 years
* Retrieval time within 12 hours

- **S3 Intelligent Tiering**

### S3 - Charges

- Storage per GB
- Requests (GET, PUT, Copy, etc)
- Storage Management Pricing
  - Inventory, Analytics, and Object Tags
- Data Management Pricing
  - Data transferred out of S3
- Transfer Acceleration
  - Use of CloudFront to optimize transfers

### S3 - Security

- By default, all newly created buckets are _private_.
- You can setup access control to your buckets using:
  - Bucket Policies (Bucket level)
    > applies to all objects within the bucket, written in JSON
  - Access Control Lists (Object level)
- S3 Buckets can be configured to create access logs, which log all requests made to the S3 bucket (these logs can be written to another bucket.)

#### Questions

- What storage type is S3, object or block. What does this mean?
- What is the file size range for S3?
- Does S3 offer unlimited storage?
- Where are files stored in S3?
- What does it mean that S3 has a universal namespace?
- What status code will you receive if you upload a file to S3 via API/CLI?
- What is the S3 data consistency for POST, PUT, DELETE?
- What is the Storage Structure of an S3 Bucket?
- What are S3 sub-resources, what are the three examples?
- What are the S3 Storage Tiers / Classes? Explain each.
- What does S3 charge for?
- Do buckets default to private or public?
- What are two levels of S3 access control?
- Can you create access logs in S3?
- Can you send access log records to other S3 buckets?

---

## Serverless 101

> evolution: Datacenter > IAAS > PAAS > Containers > Serverless

### Lambda

- A compute service where you can upload your code and create a Lambda function.
- AWS Lambda takes care of provisioning and managing the servers that you use to run the code. You don't have to worry about operating systems, patching, scaling, etc.
- Lambda can be used in the following ways:
  - **Event-driven compute service (triggers)** where AWS Lambda runs your code in response to events through API Gateway.
    EX: Changes to data in an Amazon S3 bucket, change an Amazon DynamoDB table, etc.
    EX: User adds a meme to S3 and it triggers a lambda function. It takes the picture and your text and adds the text to the image. Then another lambda function is triggered and it sends it back to the user. Lambda can trigger lambda functions.
  - Compute service to run your code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDKs.

### Languages support by Lambda

- NodeJS
- Java
- Python
- C#
- Golang

### Pricing Model

**1. Number of Requests**

- First 1 million requests are free. \$0.20 per 1 million requests thereafter.

**2. Duration**

- Duration is calculated from the time your code begins executing until it returns or otherwise terminates.
- Price depends on the amount of memory you allocate to your function. You are charged \$0.00001667 for every GB-second used.

### Exam Tips

- Lambda scales out (not up) automatically
- Lambda functions are independent, 1 event = 1 function
- Lambda is serverless
- Serverless services
  > ex: Lambda, DynamoDB, API Gateway, S3, etc.
- Lambda functions can trigger other lambda functions
- Architectures can get extremely complicated, AWS X-ray allows you to debug.
- Lambda is global, not region-locked
- Know your triggers
- No Servers
- Continuous Scaling

#### Questions

- What is Lambda?
- What are two ways Lambda can be used?
- What languages are supported by Lambda?
- What is the price model for Lambda?
- Lambda is often used through what service to direct requests?

## API Gateway

> A fully managed service that makes it easy to developers to publish, maintain, monitor, and secure APIs at any scale. You can create an API that acts as a "front door" for applications to access data, business logic, or functionality from your back-end services, such as EC2, Lambda, etc.

### API Gateway Overview

- Exposes HTTPS endpoints to define a RESTful API
- Serverless-ly connect to services like Lambda, DynamoDB, etc.
- Send each API endpoint to a different target
- Run efficiently with low cost
- Scale effortlessly
- Track and control usage w/ API key
- Throttle requests to prevent attacks
- Connect to CloudWatch to log all requests for monitoring
- Have multiple API versions

### API Gateway Config Overview

- Define an API (container)
- Define resources and nested resources (URL paths)
  - For each resource
  - Select HTTP verb
  - Set Security
  - Choose target (EC2, Lambda, DynamoDB, etc.)
- Set req/res transformations
- Deploy API to stage
  - By default, uses API Gateway domain
  - Can use custom domain
  - Now supports AWS cert manager, free SSL/TLS certs.

### API Caching

- A feature that allows API Gateway to cache endpoint responses. When cache is enabled for a stage, API Gateway caches responses from your endpoint for a specified Time-To-Live (TTL), in seconds. API Gateway then response to the request by looking up the endpoint response from the cache instead of the making a request to the endpoint.

### API Overview

- **REST APIs** - REpresentational State Transfer

  - Uses JSON
  - Much more popular than SOAP

- **SOAP APIs** - Simple Object Access Protocol
  - Uses XML
  - Old school, not _actually_ simple.

#### Questions

- What is API Gateway?
- How does Caching work in API Gateway?
- What are the main differences between REST and SOAP Apis

## DynamoDB

> A fast and flexible noSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great for a wide variety of applications.

#### Key Features

- Serverless
- Fully managed
- Supports noSQL document or key-value models.
- Can be configured to autoscale
- Well integrated with Lambda
- Always backed by SSDs
- Spread across 3 geographically distinct data centers
- 2 Consistency models:
  - Eventually Consistent Reads (default)
  - Strongly Consistent Reads (default)

#### DB Shape

- Tables
- Items (rows)
- Attributes (columns)
- Supports KV & Document data structures
- JSON, HTML or XML

#### Primary Keys

- 2 Types of Primary Key:
  - **Partition Key** - unique attribute (e.g. user ID)
  - **Composite Key** - _partition key_ + _sort key_ in combination

### Security

- Authentication and Access Control is managed using AWS IAM.
- You can create an IAM user within your AWS account which has specific permissions to create DynamoDB tables.
- You can create an IAM role that enables you to obtain temporary access keys for DDB.
- You can use special _IAM Conditions_ to restrict user access to only their own records.
  - EX: App users need to access their specific data in the database for a feature, you can add a **condition** to an IAM policy to allow access only to items where the Partition Key value matches their User ID. This restricts the user to _only_ their own data.

#### Questions

- How many model types does DynamoDB support? What are they?
- Can DynamoDB be configured to autoscale?
- What type of disc is DynamoDB backed with?
- How many geo-distinct data centers is DynamoDB spread across?
- What are the two consistency models for DynamoDB?
- What is the overall shape of a DynamoDB database?
- What languages does DynamoDB support?
- What AWS service is used to manage authentication and access for DynamoDB?
- What IAM feature can be leveraged to restrict user access within the database?
