## Elastic Transcoder

> Amazon Elastic Transcoder lets you convert digital media stored in Amazon S3 into the audio and video codecs and the containers required by consumer playback devices. For example, you can convert large, high-quality digital media files into formats that users can play back on mobile devices, tablets, web browsers, and connected televisions.

### ET Components

- **Pipelines** - queues that manage transcoding jobs. ET works through jobs synchronously. Typically, you will create two pipelines, one for standard-priority jobs and one for high-priority jobs.
- **Jobs** - specify the settings that aren't included in the preset. For example, the file to transcode and whether to create thumbnails. Each job converts one file into one different format.
- **Presets** - templates that specify most of the settings for the transcoded media file.

#### Questions

- What are the three ET components?
- Is ET synchronous?
- How can we handle low and high priority needs?

---

## Lambda

- **Triggers**
- Environment Variables

---

## RDS -- Relational Database Service

> Managed Relation Database Service in AWS

### Supported Engines

#### Commercial

- Oracle
- Microsoft SQL Server

#### Open source

- MariaDB
- PostgreSQL
- MySQL

#### Cloud Native

- Aurora (MySQL/Postgres compatible)

### Goal of RDS

- Lower the Total Cost of Ownership(TCO) by offloading routine database tasks like:
  - Provisioning
  - Patching
  - Backup
  - Recovery
  - Failure Detection
  - Repair
- Focus on core business
- Leverage AWS maturity

### Self Hosting vs RDS

#### Self Hosting

> Through EC2 or on-premise solutions

- Provision hardware
- Configure and harden OS
- Install, Setup Database and Clustering
- Create your own database
- Load data
- Tune Queries
- Design a backup strategy
- Perform patches
- Software/hardware upgrades
- Deal with failures

#### Managed by RDS

- Create Database
- Tune Queries

### Configuring RDS

- Database Engine
- License model
- DB Engine Version
- DB Instance Class
- Multi-AZ Deployment
- Storage type and size
- Backups (automatic or manual)
- Monitoring
- Maintenance Window

### Terminology

- **Database Instance**
  - Basic building block of RDS. An isolated database environment can contain multiple user-created databases
- **Instance Class**
  - Determines CPU and Memory capacity
- **Multi-AZ (aka High Availability)**
  - AZ is an isolated distinct data center
  - Multi-AZ means primary node in one AZ, the secondary backup is in another AZ
- **Read Replicas**
  - A node part of a database that only handles read queries
- **Primary Host**
  - The host / node that handles all the read and write traffic from the client
  - If Read Replicas are available, some of the read queries can be offloaded to that
- **Secondary Host (standby)**
  - The host / node within a Database Instance which is not actively handling write traffic
  - Serves as a redundancy layer in case of fail over
- **Aurora**
  - MySQL and PostgreSQL compatible relation database
  - Natively built for AWS, significant performance improvement

### Cost

- **Instance Hours**
  - Based on region, instance type, database engine, and license
- **Database Storage**
  - EBS vs Aurora, Storage Type (GP2/IO1/Magnetic), Allocation (GB)
- **Backup Storage**
  - Size up backups in AWS. No charge for storage up to 100% of total DB storage
- **Data Transfer**
  - Outgoing traffic only, regional data transfer pricing, includes copying region to region

#### Pricing Tips

    - AWS Cost Explorer
    - Using Tags to help breakdown multiple systems
    - Reserved instances where possible

### RDS Scaling

- **Scale compute/memory vertically**
  - New host is attached to existing volume
- **Scale Amazon EBS storage**
  - No downtime
- **Scale Read replicas (horizontal scaling)**
  - Only for some engines
  - Only for read traffic
  - No downtime

#### Scaling Considerations

- Ensure you have appropriate licensing if using a commercial database
- Determine when to apply the change, immediately or at a certain time
- Storage and CPU are decoupled
- Minimal downtime with MultiAZ scaling
- SingleAZ will be down during scaling operation

---

## AWS Aurora

### Performance

- Benchmarked 2x - 3x faster than standard PostgreSQL
- Benchmarked 5x faster than mySQL
- Better at scale
- Storage is up to 64 TB, grows with you (no upfront allocation required)
- Backed-up to S3 with 9x11 durability

#### Challenges with traditional DB

    - Very coupled layers
    - Slow together
    - Fail together
    - Does not scale independently
    - As strong as its weakest link

#### Aurora Solutions

    - Broke apart monolithic stack using SOA principles
    - Scale out independently
    - Self-heal and repair itself
    - Uses elastic nature of the cloud

### AWS Architecture

> Built by leveraging other AWS services

- Built with:
  - S3
  - SWF
  - DynamoDb
  - Route53
  - EC2
  - VPC
- Managed by RDS
  - Management and administrative functions
- Cloud optimized Relational Database
- Not a custom in-house database by Amazon
  - MySQL and PostgreSQL compatible

### Terminology

- **Aurora Database Cluster**
  - One or more DB instances and a cluster volume which manages the data for the instances
  - Aurora Cluster volume is a virtual database storage volume. Spanning multiple AZs, each AZ has a copy of the database cluster data
- **Two types of DB instances**
  - Primary DB Instance
  - Aurora Replicas (supports only reads)
- **Aurora DB Connections**
  - DB connections through endpoints
- **Several types of Aurora endpoints**
  - **Cluster endpoint**
    - connects to current database primary instance for the cluster. _Only_ endpoint that can provide write operations on the Database.
  - **Reader endpoint**
    - connects one of the replicas for the database cluster. Each cluster has one Reader endpoint. If there are multiple read replicas, the Reader directs each read request to one of the replicas.
  - **Custom endpoint**
    - Set of DB instances that you choose.
  - **Instance endpoint**
    - Connects to a specific database instance within a cluster. Each database endpoint within a cluster, regardless of its endpoint type, has its own unique endpoint.
    - There is one instance endpoint for the Primary instance and one instance endpoint for each Replica
- **Aurora Global Databases**
  - **Primary Region**
    - Read and Write
  - **Secondary Region**
    - Read only
    - In case of failure secondary region can be promoted

---

## VPC - Virtual Private Cloud

> Genesis: When EC2 was first introduced developers had a problem: What if their on-premise network was already using the addresses provided by the cloud? VPC gave those developers the means of manually creating private clouds that used addresses that didn't conflict with the addresses used in on-premise solutions.

- The Amazon VPC allows you to provision a logically isolated section of the cloud where you can launch AWS resources in a virtual network that you define.
  - **You have complete control of this isolated environment**
    - Select your IP address range
    - Create subnets
    - Configure route tables and network gateways
    - Use IPv4 and IPv6 in your VPC for secure and easy access to resources and applications
  - **You can easily customize the network configuration of your Amazon VPC**
    - Create a public facing subnet to for your web servers that have access to the internet
    - Place your backend systems, such as databases or application servers, in a private-facing subnet with no internet access
    - Use multiple layers of security, including security groups and network access control lists, to control access to EC2 instances in each subnet.

### Choosing address ranges

- **CIDR** (cider) - Classless Inter-Domain Routing - Used to denote a range of IP addresses
- Up to 5 CIDR ranges can be added to a VPC if you're not sure about the range.
- Defaults to IPv4. However, you can _dual-stack_ IPv4 and IPv6 by adding an IPv6 CIDR

**in action:** IPv4 - `172.31.0.0/16 === 1010 1100 0001 1111 0000 0000 0000 0000`

- The IPv4 address, when written out into binary provides a 32-bit number. The "/16" requires the first 16-bits to be static while leaving the other 16-bits to vary as needed. i.e. 172.31.x.x

#### Concepts

- Convention - following convention allow other people to understand what they're looking at.
- Warning - Avoid ranges that overlap with other networks. If you want to connect with other VPCs or other networks make sure you are not conflicting with their addresses.

### VPC Subnets

- High availability is provided through subnets. Subnets are sub-networks or sub-ranges of your VPC address base.
- VPCs are defined in a region and regions consist of multiple AZs. Your VPC exists across all the AZ within a region, and each AZ within the region has it's own self-contained subnet.
- Use multiple Availability Zones per VPC through multiple subnets.

### Route Tables

- Contain rules that determine which traffic goes where
- VPC has a default route table
- Default VPC can be overwritten with different route tables to different subnets.

### Local Access vs. Internet Access

#### Local

- Giving your VPC specific local addresses

#### Internet Gateway

- `igw-xxxxxxxxxx`

### Network Security

- Our VPC could have two sets of servers: "Web Servers" (Public Subnet) security group than accepts inbound web traffic and a "Backend" security group. The Backend servers (Private Subnet) could be set to _only_ receive traffic from Web Servers.

#### Web Servers

```
    HTTP - TCP - 80 - 0.0.0.0/0 - Allow all HTTP traffic
    HTTP - TCP - 80 - ::/0 - Allow all HTTP traffic
```

- Leverage a wildcard CIDR range to allow HTTP traffic to come from anywhere.

#### Backend Servers

```
Custom TCP Rule - TCP - 2345 - sg-xxxxxx - Allow traffic from ...
```

- The source above isn't a CIDR Range. Rather, it's another security group. This is a powerful and dynamic way to practice the "rule of least privilege". In this case, it can be set to allow only access from the Web servers without having to manually update it per every change to the web servers.

### Internet Connectivity

- Using Public and Private Subnets - Public subnet for the internet facing web servers and a Private subnet for the backend servers. The backend servers gain access to the web servers through security groups. Valid for auditing.
- Outbound-only Internet Access: **NAT (Network Address Translation)** gateway. Example: I want one of my servers from my private subnet to access resources on the internet without being routeable.
  - Use NAT from public subnet
  - Use NAT Gateway
- IPv6 does not have public/private addresses. They are globally unique.
  - Solution: Egress-Only internet gateway. Allows traffic to go out, but does not allow traffic to come in.

### Inter-VPC connectivity

- VPC Peering
  - Provide full **private IP connectivity** between two VPCs
  - Can peer VPCs **across regions**
  - VPC can be on **different accounts**
  - VPC CIDR ranges **must not overlap**

#### Questions

- What is a VPC?
- What is a subnet?
- What does CIDR stand for? What does it explain?
- How many CIDR routes can be provided to a VPC?
- Can you dual-stack IPv4 and IPv6 ranges?
- Why should you follow the address convention?
- Is a VPC defined in a region?
- What is a route table?
- What are some considerations when dealing with multiple networks?
- How can you design a VPC network that prevents your Backend servers from accessing and being accessed by the internet?
- What are two ways to achieve Outbound-only Internet Access?
- What does NAT stand for?
- Does IPv6 have public/private addresses? How is egress/ingress handled?
- What is VPC peering and what are the features of it?
- What was the genesis of VPC?
