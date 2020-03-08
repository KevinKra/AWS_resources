# AWS Solutions Architect Associate

> An Amazon certification

## Index

a. [AWS Overview](#overview-of-aws)

b. [IAM](#iam-101)

c. [S3](#s3-101)

d. [EC2](#ec2-101)

e. [Databases](#databases-on-aws)

f. [Serverless](#serverless-computing)

> Lambda, API Gateway, Alexa, X-Ray

g. [DynamoDB](#dynamo-db)

h. [KMS and Encryption](#kms-encryption)

i. [Other AWS Services](#other-services)

j. [Developer Theory](#developer-theory)

f. [Review Section](#review-section)

#### Exam blueprint

- 130 minutes in length
- 60~ questions
- Multiple Choice
- Results are between 100-1000 with a passing score of 720
- Qualification is valid for 2 years
- Scenario based questions

## Overview of AWS <a name="overview-of-aws"></a>

### The History of AWS

- Why is AWS so powerful? Amazon allows companies to use Amazon's Web Service (AWS) without the risks associated with having to build home-grown infrastructure. This allows for companies with tighter budgets to build into AWS and leverage all the integrated server scalability features that Amazon provides. Additionally, it reduces risks to the company because they no longer have to manage and maintain their own server farm.

- in 2003 Chris Pinkham and Benjamin Black presented a paper on what Amazons internal infrastructure could look like. They suggested selling it as a service and prepared a business case for it.

- SQS was launched in 2004, the very first service released by AWS.
- AWS as a business launched in 2006, targeting developers in Silicon Valley.
- by 2007, AWS had over 180,000 developers on the platform.
- by 2010, all of amazon.com moved over the AWS services.
- 2012 first re:Invent conference
- 2013 certifications released
- 2018 AWS launched Machine Learning certificates
- 2019 Alexa Specialty Beta certification launched.

### AWS Platform

- **AWS Global Infrastructure** - Amazon's global infrastructure and servers around the world. As of 2019 there are 24 regions and 72 availability zones.
- **Availability Zone** - an AZ is a data center, or cluster of data centers, that are comprised of many servers that support the AWS cloud. In many cases, there are several geographically isolated data centers that protect the network from issues that may knock any one or more centers out.
- **Regions** - A geographical area that consists of 2 or more availability zones.
- **Edge Location** - Edge locations are endpoints for AWS which are used for caching content. Caches files and content from distant regions and holds them in a closer edge location facility.

- **Amazon VPC** - Amazon Virtual Private Cloud, which is _part of Networking services_ is a virtual network dedicated to a single AWS account. It is isolated from other virtual networks in the AWS cloud, providing compute resources with robust and secure networking functionality.

### Content to focus on for certification

- Security, Identity, and Compliance
- Network & Content Delivery
- Compute
- Storage
- Databases

### Keywords:

- **Amazon VPC** - Amazon Virtual Private Cloud
- **Amazon AZ** - Availability Zone

### Questions:

- **What is a region, an availability zone, and an edge location?**

- **Where is CloudFront data cached?**

  _in Edge locations._

---

## IAM 101 <a name="iam-101"></a>

- **Identity Access Management**, IAM allows you to manage users and their level of access to the AWS console. It is important to know for administrating a company's AWS account. Allows you to create users, groups, roles, etc. on the platform and provide permissions.

### IAM features

- Centralized control of your AWS account
- Shared access to your AWS account
- Granular permissions
- Identity federations, allows end-users to potentially log in using their Facebook account, LinkedIn, etc.
- Multi-factor Authentication
- Provide temporary access for users/devices and services
- Allows password rotation policy
- Integrates with many different AWS services
- Supports PCI DSS Compliance, a compliance required for handling user data and money.

#### IAM Permissions

- **Users** - End users such as employees
- **Groups** - A collection of users, each user will inherit the permissions of the group.
- **Policies** - Policies are made up of documents called Policy documents. These documents are in JSON (JavaScript Object Notation) format and give permissions to what a User/Group/Role is able to do.
- **Roles** - You create roles and assign them to AWS resources. The resources then can communicate with other AWS services.

#### IAM Roles

- **IAM roles are more secure than storing your access and secret access keys on individual EC2 instances.**
- Roles are much easier to manage than having EC2 instances holding keys.
- Roles can be assigned to an EC2 instance after it's created using both the console and command line.
- Roles are universal, you can use them in any region.

#### Hands on

- Policy example (AdministratorAccess)

```
// Allow the user to have access to all (*) actions on all (*) resources
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

### Keywords:

- **IAM** - Identity Access Management
- **root account** - account created when we first setup AWS account. It has complete Admin access.
- **2FA** - two-factor authentication
- **MFA** - multi-factor authentication
- **Billing Alarm** - An billing limit you set that will trigger an alarm once its been reached.
- **Users**
- **Groups**
- **Policies**
- **Roles**

### Questions:

- **Is IAM limited to regions or is it universal?**

  _IAM is currently universal and does not apply to specific regions._

- **Do users have permissions when they're first created?**

  _No, new users start with NO permissions._

- **What are new users assigned when they're first created?**

  _an Access Key ID and a Secret Access Key._

- **Can you use the Access Key ID and Secret Access Key to login to the console?**

  _No, but it does allow access to AWS via APIs and the command line, or via programmatic access._

- **Describe how to disable or deactivate an access key**

  _console > IAM > Users > Security Credentials Tab > Access Keys > Status > Make Inactive_

- **Can you continue looking at the user's keys after they're generated?**

  _No, if you lose them you need to regenerate them. Save the CSV file in a secure location._

- **Should you have MFA on your root account?**

  _Yes._

- **Can you create and customize your password and pw policy rules?**

  _Yes._

- **How would you alert users in the event their billing limit has been reached?**

  _You can create a billing alarm in CloudWatch. Services > CloudWatch > Billing > Create Alarm_

### Scenarios:

- **You need to protect your account from being over-billed. How can you accomplish this?**

---

## S3 101 <a name="s3-101"></a>

> Before taking the exam read the S3 FAQS

- **Simple Storage Service**. One of the oldest services on AWS. It provides developers and IT teams with secure, durable, and highly-scalable object storage. S3 is easy to use with a simple web services interface that allows you to store and retrieve information from anywhere in the world.

### S3 Features

- S3 is **Object-based**, ie allows you to upload files.
- Files can range between 0 Bytes to 5 terabytes.
- There is unlimited storage.
- Files are stored in Buckets (directory). Must have a unique name.
- S3 is a universal name space. Names must be unique globally.
- When you upload a file to S3 you will receive an HTTP 200 code.
- Tiered Storage
- Life-cycle Management. Allows files to be moved around.
- Versioning
- Encryption
- MFA Delete
- Secure data using **Access Control Lists** and **Bucket Policies**

### S3 Objects

- **Key** - name of the object
- **Value** - data in the form of bytes
- **Version ID** - important for versioning
- **Metadata** - Data about the data
- **SubResources** - Access Control Lists, Torrent

### How does data consistency work for S3?

- Read after write for POSTs of new objects. As soon as you upload a file, you can read it.
- Eventual consistency for overwrite PUTs and DELETEs, if you wait a few moments you will be able to read the latest version.

### S3 Guarantees

- 99.99% availability guaranteed by Amazon and 99.999999999% durability. (Remember 11 9s).

### S3 Storage Classes / Tiers

- **S3 Standard** - 99.99% availability and 99.999999999% durability. Data is stored redundantly across multiple devices in multiple facilities and is designed to sustain the loss of 2 facilities concurrently.
- **S3 - IA** - Infrequently Accessed. For less frequently accessed data, but requires rapid access when needed. Lower fee than S3 standard, but you are charged a retrieval fee.
- **S3 One Zone - IA** - Infrequently Accessed. A much cheaper IA option but lacks the multiple AZ data resilience.
- **S3 Intelligent Tiering** - Leverages machine learning to automatically move data to most cost-effective access tier, without performance impact or operational overhead.
- **S3 Glacier** - Secure, durable, low-cost storage class for data archiving. You can reliably store any amount of data at costs that are cheaper than on-premises solutions. Retrieval times are configurable, can range from minutes to hours.
- **S3 Glacier Deep Archive** - Amazon S3's lowest-cost storage class. Retrieval time byte latency of 12 hours is acceptable.

### S3 Charges for

- **Storage**
- **Requests**
- **Storage Management Pricing**
- **Data Transfer Pricing**
- **Transfer Acceleration** - Allows for fast, easy, and secure transfers of files over long distances between your end users and an S3 bucket. TA takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is then re-routed to Amazon S3 over an optimized network / Amazon's backbone network.
- **Cross Region Replication** - Allows for data to be automatically replicated in another region. Allows for increased availability and provides disaster durability.

### Keywords:

- **RRS** - Reduced Redundancy Storage

### Questions:

- **What is the consistency (reading) ability for new file POSTs and existing file PUTs and DELETEs?**
  _Newly posted files can immediately be read, however editing or deleting existing files will need a brief moment to update the resource and make it readable._

- **What are the S3 Storage Classes / Tiers and what defines each tier?**

- **What are the availability and durability markings for S3 standard?**

- **What are the expenses involved with using S3 services**

- **What are the features of S3?**

- **What are the suitable types of data that can be stored on S3?**
  _It is designed to store files, not serve as a database host or installing OS._

- **What type of response does S3 send out?**

- **Can MFA be used in relation to S3?**
  _Yes, it can be used to protect from the deletion of files._

- **What are the key fundamentals of S3 Objects?**
  _There is a key, value, versionID, metadata, and sub-resources (Access Control Lists/permissions, Torrent)_

- **Explain the steps to make a file in a bucket public**

- **What happens when you make a bucket / object public?**
  _Everyone will have access to one or all of the following: read this object, read and write permissions._

- **Can the storage class be changed on the object and also on a bucket level?**
  _Yes, both buckets and individual objects can have their storage classes modified._

### S3 Security and Encryption

- By default, all newly created buckets are **private**. You can setup access control to your buckets using **Bucket Policies**. **Access Control Lists** can be used to manage access rights to objects. Additionally, S3 buckets can be configured to create access logs, which cause all requests to be logged and sent to an S3 Bucket on the same account or even on another account.

#### Encryption

- **Encryption in transit** - HTTPS is an example of encryption in transit. Achieved by **SSL/TLS**.
- **Encryption at Rest** - Can be handled server-side (amazon helps here), or client-side, where you the developer encrypt the object yourself and upload it to S3.

#### Server Side Encryption

1. **S3 Managed Keys - SSE-S3**, amazon automatically manages the keys (encryption / decryption) for you.
2. **AWS Key Management Service, Managed Keys - SSE-KMS**, developer and amazon manage the keys together.
3. **Server Side Encryption with Customer provided keys - SSE-C**, Give amazon your own keys, that you manage, and you can use them to encrypt your S3 objects.
4. **Client side encryption.** Encrypt client side and upload to S3.

### S3 Version Control

#### Features

- Stores all versions of an object, including all writes even if you delete the object.
- Great back-up tool
- Once enabled, **versioning cannot be disabled**, only suspended.
- Integrates with **Lifecycle** rules.
- **Versioning comes with with MFA delete capability** which provides another layer of security.

### Questions:

- **What happens when you utilize versioning in S3?**
  _New versions will be added with default public access set to off or private. The latest version and all previous versions will have a combined footprint in the database._

- **What happens if you delete a versioned file?**
  _A new version with a delete marker will appear. The bucket may look empty, but if you show all versions you will see previous versions (and the delete marker version) in your bucket_

- **How would you restore an object with versioning if you've already deleted it?**
  _Simple, delete the version with the delete marker and it will roll back to the latest (pre-delete) version._

### S3 Lifecycle Management and Glacier

- Lifecycles allow you to set rules to manage your objects, they can be automated to transition to tiered storage, and eventually they can be automatically set to expire based on retention needs. In short, in lifecycles automate the moving of objects between different storage tiers and can be used in conjunction with versioning (can be applied to current and previous versions).

---

## EC2 101 <a name="ec2-101"></a>

- **Elastic Compute Cloud**, Amazon EC2 is a web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, this provides for the ability to quickly scale capacity both up and down as your computing requirements change. The EC2 solution is drastically faster than traditional server solutions where setting up and deploying physical servers could take days or even months and the costs would all be upfront. EC2 allows for provisioning servers in the cloud and takes mere minutes to complete.

- Instance Metadata and User Data can be retrieved from within the instance via a special URL. Similar information can be extracted by using the API via the CLI or an SDK.

- EBS, EFS, and FSx are all storage services based on **block storage**.

- Individual instances are provisioned in AZs.

### EC2 Total Lessons Summary

#### SUMMARY: EBS

- Elastic Band Store
- EBS is basically a virtual HDD in the cloud.
- EC2 termination protection is **off** by default
- EBS-backed instances, the **default action is for the root EBS volume to be deleted** when the EC2 instance is terminated. **Additional EBS volumes will persist.**
- EBS Root Volumes of your **DEFAULT** AMI's cannot be encrypted. You can also use a third party tool to encrypt the root volume, or this can be done when create AMI's in the AWS console or using the API. Steps mentioned in notes.
- Additional, EBS volumes can be encrypted.
- Various EBS types both in SSD and HDD.

#### SUMMARY: Security Groups

- All inbound traffic is blocked by default.
- All outbound traffic is allowed.
- Changes to Security Groups take effect immediately.
- Can have multiple EC2 instances within a security group.
- Can have multiple security groups attached to EC2 instances.
- Security groups are **Stateful**, if you open a port it will be open for both inbound and outbound traffic.
- Network ACLs are **Stateless**. You will need to open _both_ the inbound and outbound traffic. Covered in VPC section.
- You cannot bock specific IP addresses using Security Groups, instead use Network Access Control Lists. Covered in VPC section.
- Can specify allow rules, but not deny rules.

#### SUMMARY: EBS Snapshots

- Volumes exist on EBS.
- Snapshots exist on S3.
- Snapshots are point in time copies of Volumes.
- Snapshots are incremental. Only blocks that have changed since your last snapshot are moved to S3.
- Your first snapshot may take some time to create. Future snapshots only replicate the deltas (changes.)
- Optional. To create a snapshot for Amazon EBS volumes that serve as root devices (where the OS is installed), you should stop the instance before taking the snapshot.
- You can create AMI's from both Volumes and Snapshots.
- You can change EBS volume sizes on the fly, including the size and storage type.
- **Volumes will ALWAYS be in the same availability zone as the EC2 instance**.

#### SUMMARY: Migrating EBS

- To move an EC2 instance volume from one AZ to another, take a snapshot of it, create an AMI from the snapshot and then use the AMI to launch the EC2 instance in a new AZ.
- To move an EC2 instance volume from one region to another, take a snapshot of it, create an AMI from the snapshot and then copy the AMI from one region to another. Then use the copied AMI to launch the new EC2 instance in the new region.

#### SUMMARY: EBS Encryption

- Snapshots of encrypted volumes are encrypted automatically.
- Volumes restored from encrypted snapshots are encrypted automatically.
- You can share snapshots, but only if they're unencrypted.
- Unencrypted snapshots can be shared with other AWS accounts or made public.
- Root Device Volumes can be encrypted. If you have an already existing unencrypted root device volumes then a series of steps need to be follow. Described in notes below.

#### SUMMARY: EBS vs Instance Store

- Instance Store Volumes are sometimes called **Ephemeral Storage.**
- Instance Store Volumes cannot be stopped. If the underlying host fails, you will lose your data.
- EBS backed instances can be stopped. You will not lose the data on the instance if it is stopped.
- You can reboot both and not lose your data.
- By default, both Root volumes will be deleted on termination. However with EBS volumes, you can tell AWS to keep the root device volume.

#### SUMMARY: CloudWatch

- CloudWatch is used for monitoring performance.
- CloudWatch can monitor most of AWS as well as applications running on AWS.
- CloudWatch with EC2 will monitor events every 5 minutes by default.
- You can have 1 minute intervals by turning on detailed monitoring.
- You can create CloudWatch alarms which trigger notifications.
- CloudWatch is about performance, CloudTrail is about auditing.
- CloundTrail monitors API calls in the AWS environment.
- Can create Dashboards.
- Can create Events.
- Can create Logs to aggregate, monitor, and store logging data.

#### SUMMARY: EFS

- Supports the Network File System 4 (NFSv4) Protocol.
- You only pay for storage you use (no pre-provisioning required.)
- Can scale up to petabytes
- Can support thousands of concurrent NFS connections.
- Unlike an EBS which can only support one EC2 instance, you can create an NFS/EFS mount and store files there and multiple EC2 instances can access it.
- Data is stored is multiple AZ's within a region.
- Read after Write consistency.

#### SUMMARY: Placement Groups

- How EC2 instances are placed.
- 3 types of placement groups: Clustered Placement Group, Spread Placement Group, Partitioned.
- Clustered Placement Group: All EC2s are in the same AZ. Low Network Latency / High Network Throughput.
- Spread Placement Group: For individual critical EC2 instances. In different AZ zones and devices.
- Partitioned: Multiple EC2 instances of HDFS, Hbase, and cassandra.
- Spread Placement Groups can be deployed across availability zones since they spread the instances further apart. Cluster Placement Groups can only exist in one Availability Zone since they are focused on keeping instances together, which you cannot do across Availability Zones
- Clustered placement does not span multiple AZ, spread and partitioned can.
- The name you specify for a placement group must be unique within your AWS account.
- Only certain types of EC2 instances can be launched in a placement group (Compute Optimized, GPU, Memory Optimized, Storage Optimized)
- AWS recommends homogenous instances within clustered placement groups.
- You **cannot** merge placement groups.
- You **cannot** move an existing EC2 instance into a placement group. You **can** create an AMI from your existing instance and then launch a new instance from the AMI into a placement group.
- Spread placement groups have a specific limitation that you can only have a maximum of 7 running instances per Availability Zone. Deploying instances in a single Availability Zone is unique to Cluster Placement Groups only.
- Depending on your type of RL(?) you can You can modify the AZ, scope, network platform, or instance size (within the same instance type), but not Region. In some circumstances you can sell RIs, but only if you have a US bank account.

### Pricing Models Instances

- **On demand** - No commitment model that allows you to pay by the hour or even second.
- **Reserved** - Provides a capacity reservation and offers a significant discount on the hourly charge for an instance. **Contract terms are 1 or 3 year terms.**
- **Spot** - Enables you to bid on excess EC2 capacity. Amazon will drop the price on EC2 instances to encourage people to use that surplus capacity. You would set price you're willing to bid at and when the prices for the EC2 instances lowers you will have access to those additional resources. As the on-demand demand goes up, the prices for those instances will go up and if they pass your price point you will lose access to them until the next occurrence of reduced prices. It's essentially a market for buying into extra resources when they're in supply.
- **Dedicated Host** - Physical EC2 server dedicated for your use. Dedicated hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.

#### On Demand Pricing

> Ideal for:

- Users that want low cost and flexibility of EC2 without any up-front payment or long-term commitment.
- Applications with short term, spiky, or unpredictable workloads that _cannot_ be interrupted.
- Applications being developed or tested on Amazon EC2 for the first time.

#### Reserved Pricing

> Ideal for:

- Applications with steady state or predictable usage.
- Applications that require reserved capacity.
- Users are able to make upfront payments to reduce their total computing cost even further.

**3 Types:**

- **Standard Reserved Instances** - Offer up to 75% off on-demand instances. The more you pay up front and the longer the contract the greater the discount.
- **Convertible Reserved Instances** - Offer up to 54% off on-demand instances and allow you to change from one reserved **EC2 Instance type** to another.
- **Scheduled Reserved Instances** - Available to launch within the time windows you reserve. This option allows you to match your capacity reservation along a predictable recurring schedule.

#### Spot Pricing

> Ideal for:

- Applications that have flexible start and end times
- Applications that are only feasible at very low compute prices
- Users with urgent computing needs for large amounts of additional capacity.
- If your spot instance is terminated by EC2, you will not be charged for partial hour usage. If you terminate the instance yourself, you will be charged for any hour which the instance ran.

#### Dedicated Host Pricing

- Useful for regulatory requirements that may not support multi-tenant virtualization.
- Great for licensing which does not support multi-tenancy or cloud deployments (like Oracle licensing).
- Can be purchased On-demand
- Can be purchased as a Reservation for up to 70% off the on-demand price.

### EC2 Instance Types

> Required knowledge for Professional Cert

**Family & Gen#** - **Specialty** - **Use case**

**F1** - Field Programmable Gate Array - Genomics research, financial analytics, real-time video processing, big data, etc.

I3 - High Speed Storage - NoSQL DBs, Data Warehousing, etc.

G3 - Graphics Intensive - Video Encoding, 3D Application streaming

H1 - High Disk Throughput - MapReduce-based workloads, distributed file systems such as HDFS and MapR-FS

T3 - Lowest Cost, General Purpose - Web Servers, small DBs

D2 - Dense Storage - Fileservers, Data Warehousing, Hadoop

R5 - Memory Optimized - Memory Intensive Apps/DBs

M5 - General Purpose - Application Servers

C5 - Compute Optimized - CPU intensive Apps/DBs

P3 - Graphics/General Purpose GPU - Machine Learning, Bit Coin Mining, etc.

X1 - Memory Optimized - SAP HANA / Apache Spark, etc.

Z1D - High compute capacity and a high memory footprint - Ideal for Electronic Design Automation (EDA) and certain relational databases with high per-core licensing costs.

A1 - Arm-based workloads - Scale-out workloads such as web servers

U-6tb1 - Bare Metal - Bare metal capabilities that eliminate virtualization overhead.

**Mnemonic**

> FIGHT DR MCPXZ AU

**F** - for FPGA

**I** - for IOPS

**G** - Graphics

**H** - High Disk Throughput

**T** - Cheap general purpose

**D** - for Density

**R** - for RAM

**M** - Main choice for general purpose apps

**C** - for Compute

**P** - Graphics

**X** - Extreme Memory

**Z** - Extreme Memory && CPU

**A** - Arm-based workloads

**U** - Bare Metal

### SSH into EC2 Instance and Setup Webserver

#### Steps (Mac):

1. `cd downloads`
2. `mkdir SSH`
3. `mv <KeyPair> SSH` - move .pem file to SSH directory
4. `cd SSH`
5. `CHMOD 400 <KeyPair>` - lockdown file
6. `ssh ec2-user@<our-ip-address> -i <KeyPair>` - Gain access to ec2 user account.

7. yes
8. permanently adds your ip address to the list of known hosts for the EC2 Instance.

9. `sudo su` - Elevates privileges from ec2-user to root
10. `yum update -y` - looks for OS updates
11. `yum install httpd -y` - installs Apache, turns EC2 instance into a webserver.
12. `cd /var/www/html` - Anything put in here will essentially be a website.
13. `nano index.html` - Create html doc in nano text editor
14. `service httpd start` - launches the webserver so you can visit the website.
15. `chkconfig on` - automatically starts the httpd service if your ec2 instance reboots.

### Security Groups Basics

- Every time you make a rule change in a security group, that change takes affect immediately. If you delete your inbound HTTP port 80 rules you will immediately lose the ability to access the website.
- **Security Groups are stateful**, when you create an inbound rule an outbound rule is created automatically. If you allow HTTP, SSH, etc. in, it is automatically allowed back out.
- Security groups work by blocking everything by default, you as the developer have to _allow_ traffic like HTTP, mySQL, etc. to go through.
- All inbound traffic is blocked by default.
- All outbound traffic is allowed.
- Changes to security groups take effect immediately.
- You can have multiple security groups attached to EC2 Instances.
- You can specify allow rules, but not deny rules.

### Keywords:

- **AMI** - Amazon Machine Image

### Questions:

- **Explain EC2.**

- **How many different instance price models are there and what are their details?**

- **How many types of reserved instances exist and what are their details?**

- **What are the EC2 types and their respective use cases?**

- **Is termination protection on or off by default?**
  _By default EC2 termination protection is off_

- **On an EBS-backed instance, is the default action to delete the root EBS volume when the instance is deleted?**
  _Yes. If you terminate your EC2 instance you're also going to terminate your virtual HDD as well. Can be changed to not do this._

- **Can the EBS Root Volumes of your DEFAULT AMI's be encrypted?**
  _No, but third party tools (like bit locker) can be used to encrypt the root volume_

- **Can additional EC2 instance volumes be encrypted?**
  _Yes._

- **Which EC2 volume is the device OS installed onto?**
  _The root volume_

- **If you make a rule change to a security group, how quickly does it take affect?**
  _Immediately._

- **What happens if you delete an outbound rule in an EC2 instance?**
  _Nothing, security groups are stateful. When you create an inbound rule an outbound rule is automatically created._

- **Can you blacklist ports or IP addresses with security groups?**
  _Nope. That said, security groups work by blocking everything by default, you as the developer have to allow traffic access manually. In order to block specific IP addresses you would use Network Access Control Lists_

- **Can you attach more than one security group to an EC2 instance?**
  _Yes. Actions > Networking > Change Security Groups_

---

## EBS 101

- What is EBS? **Elastic Block Store**, it provides persistent block storage volumes for use with Amazon EC2 instances in the AWS cloud. **Each Amazon EBS volume is automatically replicated within its AZ to protect you from component failure**, offering high availability and durability. In short, EBS is a virtual HDD in the cloud.

### 5 Types of EBS Storage

> gp2, io1, st1, sc1, standard

- **General Purpose (SSD)** - **gp2** - Balance of price and performance suitable for most workloads.
  > _Volume Size: 1 GiB - 16 TiB, Max IOPS Volume: 16,000_
- **Provisioned IOPS (SSD)** - **io1** - Highest Performance SSD volume designed for mission-critical applications.
  > _Volume Size: 4 GiB - 16 TiB, Max IOPS Volume: 64,000_
- **Throughput Optimized HDD** - **st1** - Lost cost HDD volume suitable for Big Data & Data Warehouses
  > _Volume Size: 500 GiB - 16 TiB, Max IOPS Volume: 500_
- **Cold HDD** - **sc1** - File Servers
  > _Volume Size: 500 GiB - 16 TiB, Max IOPS Volume: 250_
- **EBS magnetic HDD** - **standard** - Workloads where data is infrequently accessed and not using something like S3 Glacier.
  > _Volume Size: 1 GiB - 1 TiB, Max IOPS Volume: 40-200_

### Volumes and Snapshots

- Volumes exist on EBS. Think of EBS as a virtual hard disk.
- **Snapshots exist on S3**. Think of snapshots as a photograph of the disk.
- Snapshots are point-of-time copies of Volumes.
- Snapshots are incremental -- this means that only the blocks that have changed since your last snapshot are moved to S3.
- The first snapshot takes some time to create.
- To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot to ensure it is consistent. Though, it can still be taken while the instance is running.
- You can create AMI's from both Volumes and Snapshots.
- You can change EBS volume sizes on the fly, including changing the size and storage type.
- Volumes will **ALWAYS** be in the AZ as the EC2 instance.
- **EC2 AZ change:** EC2 volumes can be moved from one AZ to another. To move an EC2 volume, take a snapshot of it, create an AMI from the snapshot, then use the AMI to launch the EC2 instance in a new AZ.
- **EC2 Region change:** Take a snapshot of the EC2 volume, create an AMI from the snapshot, copy the AMI from one region to another. Then use the copied AMI to launch the new EC2 instance in the new region.

### EBS vs Instance Store

- Instance Store Volumes are sometimes called Ephemeral Storage.
- **Instance Store Volumes cannot be stopped.** If the underlying host fails, you will lose your data.
- **EBS backed instances can be stopped.** You will not lose your data on the instance if it is stopped.
- You can reboot both an instance store volume and an EBS backed instance, you will not lose your data. Essentially, only if the host fails and your data is stored on an instance store than you will lose your data.
- By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume. That cannot be done with an instance store.

#### AMI can be selected based on:

- Region
- Operating System
- Architecture (32-bit, 64-bit)
- Launch Permissions
- Storage for Root Device (Root Device Volume)

  1. Instance Store (**EPHEMERAL STORAGE**)
  2. EBS Backed Volumes

- All AMIs are categorized as either backed by Amazon EBS or backed by instance store.
- **For EBS Volumes:** The root device for an instance launched from the AMI is an Amazon EBS Volume created from an Amazon EBS snapshot.

- **For Instance Store Volumes:** The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3.

### Encrypted Root Device Volumes & Snapshots

- **The old school way of encrypting a EC2 instance's Root Device Volume:** take a snapshot of the (unencrypted) root volume, copy the snapshot and enable encryption, then create an AMI from that snapshot, then launch that EC2 instance as an encrypted root device volume.

- In the past you were not able to have encrypted root device volumes, so you had to follow the above work-around steps to encrypt it. These days, you can launch a root device volume with encryption.

- You cannot take a snapshot that is encrypted and then launch it as a non-encrypted volume.
- Snapshots of encrypted volumes are encrypted automatically.
- Volumes restored from encrypted snapshots are encrypted automatically.
- You can share snapshots, but **only** if they're unencrypted.
- Unencrypted snapshots can be shared with other AWS accounts or made public.
- You can now encrypt root device volumes upon creation of the EC2 instance.

### Questions:

- **Can you have your EC2 and EBS volumes in different AZs?**  
  _No. When you have a virtual machine, you would want the virtual hard drive to be as close as possible, so having them in the same location is a logical conclusion._

- **How do you move an EDS volume to a new location?**

- **When you terminate an EC2 instance will the root and EBS volumes all terminate?**
  _No. When you terminate an EC2 instance only the root volume will terminate with it. You will need to manually terminate additional EBS volumes that you had provisioned._

- **You have an already existing unencrypted root device volume, what is the process for encrypting it?**

---

## EFS 101

- Amazon **Elastic File System** is a file storage service for Amazon Elastic Compute Cloud (EC2) instances. Amazon EFS is easy to use and provides a simple interface that allows you to create and configure file systems quickly. With Amazon EFS, storage capacity is elastic, growing and shrinking automatically as you add and remove files, so your applications have the storage they need, when they need it.

- Similar to EBS except with EBS you can only mount your disk to one EC2 instance. You cannot have two EC2 instances one EBS volume. However, you _can_ have two EC2 instances share an EFS volume.

- If you provision an EFS instance, unlike an EBS volume, it will grow dynamically with the EC2 instance.

---

## CloudWatch 101

- CloudWatch is a monitoring service used to monitor your AWS resources, as well as the applications that you run on AWS. CloudWatch basically monitors performance.

#### Can monitor things like:

- **Compute**
  - EC2 Instances
  - Autoscaling Groups
  - Elastic Load Balancers
  - Route53 Health Checks
- **Storage & Content Delivery**
- EBS Volumes
- Storage Gateways
- CloudFront

#### Monitors Host Level Metrics like:

- CPU
- Network
- Disk
- Status Desk
  - Underlying hypervisor
  - Underlying EC2 instance

#### Cloudtrail vs Cloudwatch monitoring

- **AWS Cloudtrail** increases visibility into your user and resource activity by recording AWS management console actions and API calls. You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the calls occurred.

- Essentially, when you create an EC2 instance, S3 bucket, etc. you are making an API call to AWS. This actions are recorded by Cloudtrail.

- **AWS Cloudwatch** is used for monitoring performance. Can monitor most of AWS as well as applications run on AWS.
- Cloudwatch with EC2 will monitor events every 5 minutes by default.
- Can activate detailed monitoring turn on with 1 minute intervals.
- Can create Cloudwatch alarms. ex: Billing Alarm.
- CloudWatch is about performance. CloudTrail is auditing.

### Cloudwatch Features

- Standard Monitoring = 5 minutes
- Detailed Monitoring = 1 minute

- **Dashboards** - create dashboards to track AWS environment.
- **Alarms** - Allows you to create alarms when threshold limits are reached.
- **Events** - Cloudwatch events respond to state changes in your AWS resources.
- **Logs** - Cloudwatch logs help you aggregate, monitor, and store logs.

---

## AWS CLI

- Can interact with AWS from anywhere in the world just by using the CLI
- You will need to set up access in IAM
- **IAM roles are more secure than storing your access key and secret access keys on individual EC2 instances.**
- Roles are much easier to manage than having EC2 instances hold keys.
- Roles can be assigned to an EC2 instance after is created using both the console and command line.
- Roles are universal, you can use them in any region.

#### useful commands:

`aws <service> ls`
`aws configure`
`aws s3 mb s3://<bucketname>` - make bucket
`cd ~` - home directory
`cd .aws` - hidden aws directory containing your config and credentials (Access key and Secret key here.)
`rm -rf .aws` - removes hidden aws directory and removes credentials

---

### Boot Strap Scripts

`#!/bin/bash`

> Note: there seems to be a potential error in the below bash commands

```
#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
echo "<html><h1>Hello this is another webpage</h1></html>"
> index.html
aws s3 mb s3://hjkhjkhjkqweide123asddddWOW
aws s3 cp index.html s3://hjkhjkhjkqweide123asddddWOW
```

---

## Databases on AWS <a name="databases-on-aws"></a>

- Relational databases have existed since the 1970s, they are a series of interconnected tables with one-to-one, one-to-many, and many-to-many (that utilize join tables) relationships. Relational databases consist of tables or **collections** which themselves consist of rows. Rows, or **documents**, consist of key-value pairs or **fields**.

#### Six relational databases on AWS

- SQL Server (Microsoft)
- Oracle
- MySQL
- PostgreSQL
- Amazon Aurora
- MariaDB

#### RDS has two key features (RDS - Relational Database Services)

- **Multi-AZ** - for disaster recovery. If we lost access to one AZ amazon would detect that and update the DNS to point to the secondary address's IP address.
- **Read Replicas** - For performance. Every time you do a write to a database, the write will be automatically copied to the other database. However, there is no automatic fail-over from one database to the other database holding the copies. You would need to create a new url and point your EC2 instance to point at replica. Replicas are useful for scaling your database, if your website becomes extremely popular you could point half of your instances to read from the replica. **You can have five copies of read-replicas.**

### DynamoDB

- Amazon DynamoDB is a fast and flexible noSQL database service. It is designed for applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and **supports both document and key-value data models.** Its flexible data model and reliable performance make it a great fir for mobile, web, gaming, ad-tech, IoT, and many other applications.

#### Features

- Stored on SSD storage
- Spread across 3 geographically distinct data centers
- **Eventual Consistent Reads** (Default) - consistency is reached across all copies of data usually within 1 second. For applications that _don't_ need immediate write to read consistency.
- **Strongly Consistent Reads** - When you write to DynamoDB table and you need to read that data within or less than 1 second. Essentially, will return a result that reflects all writes that received a successful response prior to the read. For applications that need immediate write to read consistency.

---

## Serverless Computing <a name="serverless-computing"></a>

> Data Center >> IAAS(AWS) >> PAAS(ELastic Beanstalk) >> Containers >> Serverless

## Lambda

> Data Center >> Hardware >> Assembly Code/Protocols >> High Level Languages > Operating Systems > Application Layer/AWS APIs > AWS Lambda

AWS Lambda is a compute service where you can upload your code and create a Lambda function. AWS Lambda takes care of provisioning and managing the servers that you use to run the code. You don't have to worry about operating systems, patching, scaling, etc.

- Can be used as an event-driven compute service where Lambda runs code in response to events.
- As a compute service to run code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDKs.

### Lambda Pricing

- First 1-million requests are free. \$0.20 per 1-million requests thereafter.
- Duration, calculated from the time your code begins executing until it returns or otherwise terminates. Rounded up to the nearest 100 millisecond. The price depends on the amount of memory you allocate to your function. You are charged \$0.00001667 per GB-second used.

### Lambda Version Control

When you use versioning in AWS Lambda, you can publish one or more versions of your Lambda function. As a result, you can work with different variations of your Lambda function in your development workflow, such as development, beta, and production. Each Lambda function version as a unique **Amazon Resource Name (ARN).** After you publish a version it is immutable.

- AWS Lambda maintains your latest function code in $LATEST. You _can_ edit the **$LATEST\*\* version. When you update your function code, AWS Lambda replaces the code in the \$LATEST version of the Lambda function.

- Qualified ARN: The function with the suffix \$LATEST
- Unqualified ARN: The function without the version suffix

### Alias

- After initially creating a Lambda function you can publish a version 1 of it. By creating an alias named PROD that points to version 1, you can now use the PROD alias to invoke version 1 of the Lambda function. Now, you can update the code (\$LATEST) with all of your improvements and then publish another stable and improved version (version 2). You can promote version 2 to production by remapping the PROD alias so that it points to version 2. If you find something wrong you can easily roll back the production version to version 1 by remapping the PROD alias so that it points to version 1.

#### Key Features

- No Servers
- Continuous Scaling
- Extremely cheap

#### Lambda Triggers

- API Gateway
- AWS IoT
- Alexa Skills Kit
- Alexa Smart Home
- Application Load Balancer
- CloudFront
- CloudWatch
- CodeCommit
- Cognito Sync Trigger
- DynamoDB
- Kinesis
- S3
- SNS
- SQS

### Step Functions

- Step Functions allow you to visualize and test your serverless applications. Step Functions provide a graphical console to arrange and visualize the components of your application as a series of steps. This makes it simple to build and run multistep applications. Step Functions automatically trigger and tracks each step, and retries when there are errors, so your application executes in order and as expect. It logs the state of each step, so when things go wrong , you can diagnose and debug problems quickly.

- **Sequential Steps** - upload file and then delete it
- **Branching Steps** (Choice of Path) - select image format > load in database > end.
- **Parallel Steps** - Process photo > trigger three functions to resize, facial recognition, extract meta data > then store data.

- Great way to visualize a serverless application
- Step functions automatically trigger and track each step
- Step functions log the state of each step so if something goes wrong we can track it.

### X-Ray

- AWS X-Ray is a service that collects data about requests that your application serves, and provides tools you can use to view, filter, and gain insights into that data to identify issues and opportunities for optimization. For any traced request to your application, you can see detailed information not only about the request and response, but also about calls that your application makes to downstream AWS resources, microservices, databases, and HTTP web APIs.

#### X-Ray Architecture

- **X-Ray SDK**
  - installed inside of application
  - sends data to X-Ray Daemon
- **X-Ray Daemon**
  - Listens on UDP and send JSON over to X-Ray API
- **X-Ray API**
  - Stores data and creates X-Ray visualization
- **Scripts and Tools**
  - Communicate with Daemon or API directly

#### X-Ray SDK

> XXXXXXXXXXXXXXXXXXXXXX

##### NOT FINISHED !!!!

- The X-Ray SDK provides:
- Interceptors to add to your code to trace incoming HTTP requests
- Client handlers to instrument AWS SDK clients that your application uses to call other AWS services
- An HTTP client to use to instrument calls to other internal and external HTTP web services
- Integrates with ELB, Lambda, API Gateway, EC2, Elastic Beanstalk

#### X-Ray Supported Languages

- Java, Go, Node, Python, Ruby, .net

#### Exam Blueprint

- Lambda scales out (not up) automatically
- Lambda functions are independent, 1 event = 1 function
- Lambda is serverless
- Serverless services: Lambda, API Gateway, DynamoDB, Serverless-Aurora, etc
- Lambda functions can trigger other lambda functions
- Architecture can get complicated. AWS X-ray allows you to debug lambda
- Lambda can do things globally
- Know your lambda triggers
- You can have multiple versions of Lambda function
- Latest version will use \$latest
- Qualified version will use \$latest, unqualified will not have it
- Versions are immutable
- Can split traffic using aliases to different versions
- Cannot split traffic with \$latest, instead create an alias to latest
- S3 buckets can be used globally but are handled on a regional basis
- Step functions are a great way to visualize your serverless application
- Step functions automatically trigger and track each step
- Step functions log the state of eah step so if something goes wrong you can track what went wrong and where
- X-Ray interceptors are added to code to trace incoming HTTP requests
- X-Ray client handlers to instrument AWS SDK clients that your application uses to call other AWS services
- X-Ray an HTTP Client to use instruments calls to other internal or external HTTP web services
- X-Ray integrates with: Lambda, ELB, API Gateway, EC2, Elastic Beanstalk
- X-Ray integrates with: Java, Go, Node.js, Python, Ruby, .Net

### Questions:

- **What is Lamda?**
- **What are two ways to implement Lambda?**
- **How many initial requests are free, what is the price thereafter?**
- **Explain the duration pricing for Lambda.**
- **What are three key features of Lambda?**
- **Does Lambda scale up automatically?**
- **Are lambda functions independent?**
- **Are there any RDS types that are serverless?**
- **What AWS service allows for you to debug Lambda?**
- Can lambda functions trigger other lambda functions?
- **Is lambda global or regional?**
- What are the lambda triggers?
- Explain lambda version control.
- What is ARN?
- Where does lambda store your latest code?
- What is lambda alias?
- What does the qualified lambda version end with?
- What does the unqualified lambda version end with?
- **What are step functions?**
- **What are the three types of step functions?**
- What does AWS X-ray help resolve?
- Can lambda be used globally, is it handled locally?
- What are Step functions and what benefits does it provide?
- Explain X-Ray.
- What services does X-Ray integrate with?

## API Gateway

- API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale. With a few clicks you can create an API that acts as a "front door" for applications to access data, business logic, or functionality, from your back-end services such as applications running on EC2 code running on AWS Lambda, or any other web application.

- REST APIs - REpresentational State Transfer - uses JSON
- SOAP APIs - Simple Object Access Protocol - uses XML

Handling SOAP - SOAP applications send their responses in XML format. API Gateway supports SOAP applications but only provides passthrough.

#### Key Features

- Exposes HTTPS endpoints to define a RESTful API
- Serverlessly connect to services like Lambda and DynamoDB
- Send each API endpoint to a different target
- Run efficiently with low cost
- Scales effortlessly
- Track and control usage by API key
- Throttle requests to prevent attacks
- Connect to Cloudwatch to log all requests for monitoring
- Maintain versions of your API

#### Configuration

- Define an API (container)
- Define resources and nested resources (URL paths)
- For each Resource:
  - Select supported HTTP methods (verbs)
  - Set security
  - Choose target (EC2, Lambda, DynamoDB, etc.)
  - Set request and response transformations
- Deploy API to a Stage (prod, test, deploy)
  - Uses API Gateway domain, by default
  - Can use custom domain
  - Supports AWS Certificate Manager: free SSL/TLS certs!

#### API Caching

- You can enable API Caching in Amazon API Gateway to cache your endpoint's response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then response to the request by looking up the endpoint response from the cache instead of making a request to your endpoint.

#### API Throttling

- By default, API Gateway limits the steady-state request rate to **10,000 requests per second**
- **The maximum concurrent requests is 5000 requests** across all APIs within an AWS account
- If you go over 10,000 RPS or 5000 concurrent requests you will receive a **429 Too Many Requests** error response

#### Same-Origin Policy

**Same-origin policy** is a web policy where a web browser permits scripts contained in a first web page to access data in a second webpage, but only if both webpages have a same origin.

#### Cross-Origin Resource Sharing (CORS)

**CORS** is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain which the first resource was served.

#### Import APIs

- You can use the **API Gateway Import** API feature to import an API from an external definition file into API Gateway. Currently, the import API feature supports Swagger v2.0 definition files
- API can be updated with POST or PUT

### Exam Blueprints

- API Gateway has caching capabilities
- API Gateway is low cost and scales automatically
- You can throttle API Gateway to prevent attacks
- You can log results to CloudWatch
- If you are using JS that uses multiple domains with API Gateway, ensure you enable CORS on API Gateway
- CORS is enforced by the client
- API Gateway _can_ be configured as a SOAP web-service passthrough
- Where can you log results to?
- Swagger is used to leverage an existing API within AWS

### Questions:

- **What is API Gateway?**
- **What are two types of API Design, what language does each use?**
- **What are some key features of API Gateway?**
- **What is the general configuration of API Gateway?**
- **What is API Caching?**
- **Explain CORS.**
- Can API Gateway throttle DDOS attacks?
- How does API Gateway deal with legacy SOAP applications?
- What is the Swagger tool used for?

---

## DynamoDB

Amazon DynamoDB is a fast and flexible noSQL database service for all applications that need consistent, single-digit millisecond latency, at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

- Stored on SSD storage
- Spread across 3 geographically distinct data centers
- Choice of two consistency models:

  - Eventual Consistency Reads (default)
  - Strongly Consistent Reads

- Data is stored in Tables, Items (rows), Attributes (column)
- Documents can be written in JSON, HTML or XML

#### Primary Keys

- Two types:
  - **Partition Key** - unique attribute (user ID)
    - value of the Partition key is input as an internal hash function which determines the partition or physical location on which the data is stored
    - if you are using the partition key as your primary key, then no two items can have the same partition key
  - **Composite Key** - Partition key + Sort key
    - User Id + Time stamp of the post (Sort Key)
    - Allows you to store multiple items with the same Partition Key

```
{
  "userId": 19311,   // Partition Key
  "firstName": "Allen",
  "lastName": "Worchester",
  "courseName": "AWS_Developer_Associate"  // Sort Key
}
```

#### Access Control

- Authentication and Access Control is managed through AWS IAM
- You can create an IAM user within your AWS account which has specific permissions to create DynamoDB tables
- You can create an IAM role which enables you to obtain temporary access keys which can be used to access DynamoDB
- You can use a special **IAM Condition** to restrict user access _only_ to their own records

### Exam Tips:

- DynamoDB is a low latency NoSQL database
- Consists of Tables, Items, and Attributes
- Supports both document and key-value data models
- Supports JSON, HTML, XML
- 2 Types of Primary Key - Partition Key / Partition Key + Sort Key (Composite Key)
- 2 consistency models: strongly consistent / eventually consistent
- Access is controlled with IAM policies
- `dynamodb:LeadingKeys` allows users to access only the items where the partition key values matches their user ID

### Questions:

- Describe DynamoDB
- What data models does DynamoDB support?
- What type of Hard drive does DynamoDB use?
- How many data centers is data stored across?
- What are the two consistency models?
- What are the two types of primary keys, explain each and a use case.
- What are four ways to handle access control?
- What is a use case for using IAM Conditions in DynamoDB?
- What languages does DynamoDB support?
- How is access handled with DynamoDB

---

## Review Section

> This section is designed to provide a comprehensive review of the entire lesson. Questions are written more as statements or keywords and designed to be talked about by yourself or with a partner. You should aim to speak confidently about the topics and review material when needed. Be honest with your results.

- What risks does AWS mitigate for businesses?
- Why is AWS suitable for both small start ups and large companies?
- When was AWS launched?
- What were AWS certificates released?
- What is AWS Global infrastructure?
- What is an Availability Zone?
- What is an AWS Region?
- What are Edge Locations?
- Explain Amazon VPC.
- Where is CloudFront data cached?
- What does IAM stand for, what is its purpose?
- What are identity federations?
- What are the 4 IAM permission types?
- Explain each IAM permission type.
- What format are policy documents written in?
- What does JSON stand for?
- What is a billing alarm?
- What is a root account, what permissions does it have?
- Explain the steps to setup a billing alarm.
- Is IAM limited to a region or is it universal, why?
- Do users have permissions when they're first created?
- What are users assigned when they're first created?
- Can you use the Access Key ID and Secret Access Key to login into the console?
- Explain the process to disable or deactivate an access key.
- Can you continue to look at a user's keys after they're generated?
- Should you have MFA on your root account?
- Explain the process for creating and customizing password policy rules.
- How would you protect your account from being over-billed?
- What does S3 stand for?
- Describe S3.
- S3 is Object based. What does that mean?
- What is the file size range for files uploaded to S3?
- Does S3 allow unlimited storage?
- What is the name used for directories in S3?
- What is the name of data stored in S3 directories?
- S3 is a universal name space, what does that mean?
- What kind of response do you receive when you upload a file to S3?
- Explain tiered storage.
- Explain life-cycle management in S3.
- Explain versioning in S3.
- Explain encryption in S3.
- What does MFA Delete mean and why is it important?
- What are Access Control Lists and Bucket Policies, what are they for?
- S3 Objects have several (5) values associated with them, what are they?
- What is data consistency?
- How does data consistency work in S3?
- What is S3's guarantee?
- What are the S3 Storage classes / S3 Storage tiers.
- Explain S3 Standard, what it is suitable for?
- Explain S3 - IA, what it is suitable for?
- Explain S3 One Zone - IA, what it is suitable for?
- Explain S3 Intelligent Tiering, what benefits does it provide?
- Explain S3 Glacier, what it is suitable for?
- Explain S3 Glacier Deep Archive, what it is suitable for?
- What 5 things does S3 charge for?
- What is transfer acceleration, how does it work?
- What is cross region replication, how does it work?
- What does RRS stand for?
- Can MFA be used in S3, in what regard?
- What is S3 designed for, is it suitable for databases?
- What happens if you make a bucket / object public?
- Can buckets and objects have their respective storage classes modified?
- What is the default public setting for new buckets?
- What can you use to control access to your bucket?
- Can access logs be created for buckets? Where can the logs be stored?
- What is encryption in transit, what is an example?
- SSL/TLS are used for what type of encryption?
- What is Encryption at Rest, what two environments can it be handled?
- What are the four types of server-side encryption?
- Explain SSE-S3.
- Explain SSE-KMS.
- Explain SSE-C.
- Explain Client Side encryption.
- What is S3 Version Control.
- Can S3 versioning be disabled once initiated?
- Can S3 versioning be suspended?
- Can S3 versioning be integrated with lifecycles rules?
- Can S3 versioning come with MFA delete capability?
- What happens when you utilize versioning in S3?
- What happens if you delete a versioned file?
- How would you restore an object with versioning if you've already deleted it?
- What do S3 Lifecycles accomplish, how would they interact with versioning?
- What does EC2 stand for?
- What does EC2 accomplish?
- What were the challenges that EC2 solved?
- What are the 4 pricing models for EC2?
- Explain each EC2 pricing model in detail.
- What is the On Demand model suitable for?
- What is the Reserved model suitable for?
- What are the 3 types of reserved instances?
- What is the Sport Pricing model suitable for?
- What is the Dedicated Host model suitable for?
- What is the EC2 Instance Type mnemonic phrase?
- What are the 14 EC2 Instance types, what are they suitable for?
- Relational databases are comprised of what?
- What 6 relation databases are supported by AWS?
- What does RDS stand for?
- What are the two key features that RDS provides?
- Explain Multi-AZ.
- Explain Read Replicas.
- What is DynamoDB?
- What are the 4 features of DynamoDB?
- Is EC2 termination protection on or off by default?
- On an EBS-backed instance, is the default action to delete the root EBS volume when the instance is deleted?
- Can the EBS Root Volumes of your DEFAULT AMI's be encrypted?
- Which EC2 volume is the device OS installed onto?
- Security Groups are stateful, what does that mean?
- If you make a rule change to a security group, how quickly does it take affect?
- What happens if you delete an outbound rule in an EC2 instance?
- Can you blacklist ports or IP addresses with security groups?
- Can you attach more than one security group to an EC2 instance?
- If an Amazon EBS volume is an additional partition (not the root volume), can I detach it without stopping the instance?
- Can you add multiple volumes to an EC2 instance and then create your own RAID 5/RAID 10/RAID 0 configurations using those volumes.
