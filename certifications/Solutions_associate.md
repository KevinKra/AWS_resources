## IAM - Identity Access Management

### Key Features

- Centralized control of account.
- Shared access to IAM account
- Granular Permissions
- Identity Federation (Active Directory, Facebook, LinkedIn, etc)
- Multifactor Authentication
- Provide Temporary access for users/devices
- PSCI DSS Complaint

### Key Terms

- **Users**
  - End users
- **Groups**
  - Collection of users
- **Policies**
  - JSON policy documents
- **Roles**
  - Assigned to AWS resources

---

## S3 - Simple Storage Service

### Key Features

- Object-based
- 0-5TB files
- Unlimited Storage
- Stored in Buckets
- Universal name space
- Receive 200 HTTP code on success

#### Object Based

- Key
- Value
- Version ID
- Metadata

### Consistency

- **POST** - Read after Write (Immediate)

- **PUT/DELETE** - Eventual Consistency (Delayed)

### Guarantees

- Built for 99.99% availability, _Amazon guarantees 99.9%._
- 9x11 Durability guaranteed.

### Management

- Tiered Storage
- Lifecycle Management
- Versioning
- Encryption (even at rest)
- MFA for deletion
- Access Control Lists
- Bucket Policies

### Storage Classes

- **S3-Standard**
  - Immediate Access
  - Data is redundantly stored across multiple devices in multiple facilities.
  - Designed to sustain the loss of 2 facilities concurrently.
- **S3-IA**
  - Infrequently accessed data that still requires immediate retrieval.
  - Lower fee than S3-standard, but you are charged a retrieval fee.
- **S3 One Zone-IA**
  - Lower cost option than S3-IA.
  - Does not have data resilience of other classes.
- **S3-Intelligent Tiering**
  - Designed to optimize costs by automatically moving data to most cost-effective tier.
  - No performance or operational overhead.
- **S3 Glacier**
  - Archive.
  - Very cheap.
  - Retrieval time from minutes to hours.
- **S3 Glacier Deep Archive**
  - Archive.
  - Cheapest.
  - 12-hour response time is acceptable.

### Billing

- Storage
- Requests
- Storage Management Pricing (Tiers)
- Data Transfer Pricing
- Transfer Acceleration
- Cross Region Replication

### Cross Region Replication

- When you upload data in one bucket, it is automatically replicated in another bucket elsewhere.
- Replicates Data for HA and disaster recovery.

### Transfer Acceleration

- Enables fast, easy, and secure transfers, over CloudFront's globally distributed edge locations. As the data arrives at an EdgeFront location the data is routed to Amazon S3 over an optimized network path.

#### Questions

- What type of object storage is S3?
- How large/small can S3 files be?
- What are files called in S3?
- How much data can you store in S3?
- What type of namespace does S3 have?
- What are the four aspects of S3 objects?
- Do you receive a status code on uploads? Which?
- What is the S3 consistency for POST?
- What is the S3 consistency for PUT/DELETE?
- What is the Amazon guaranteed availability and durability?
- What are the six storage tiers? Explain each?
- What are the six billing parameters?
- Explain Cross Region Replication.
- Explain Transfer Acceleration.
- Is S3 suitable for installing an OS or hosting a DB?

---

## EC2

---

## Databases

---

## Route53

---

## VPCs

---

## HA Architecture

---

## Applications

---

## Serverless

---
