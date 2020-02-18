## VPC overview

> A virtual data center in the cloud

- ex: EC2 instances are deployed into our default VPC. Everyone region in the world has a default VPC.

```
// General Implementation
Internet Gateway(IGW)/Virtual Private Gateway(VPG) => Router => Route Table => Network ACL => Public/Private Subnet + (Security Group + Instance)
```

### What can you do with a VPC

- Launch instances into a subnet of your choosing.
- Assign custom IP address ranges in each subnet.
- Configure route tables between subnets.
- Create internet gateway and attach it to your VPC.
- Much better security control over AWS resources.
- Instance security groups.
- Subnet network Access Control Lists (ACLs.)

### Default VPC vs Custom VPC

- Amazon provisions an default VPC in every region.
- Default VPC is user friendly, allowing you to immediately deploy instances.
- All subnets in default VPC have a route to the internet, no private subnets in default VPCs.
- Each EC2 instance has a both public and private IP address.

### VPC Peering

- Allows VPCs to connect to another via direct network route using private IP addresses.
- Instances behave as if they were on the same private network.
- You can peer VPCs with other AWS accounts as well as the same account.
- Peering is int a star configuration. 1 central VPC peers w/ 4 others. **NO TRANSITIVE PEERING**.

### Exam Tips

- VPC consists of IGWs/VPGs, Route Tables, Network Access Control Lists, Subnets, and Security Groups
- 1 Subnet = 1 AZ
- Security Groups are Stateful
- Network ACLs are stateless
- No transitive peering

---

## VPC Components

### Global Terms

- **CIDR block** - Classless Inter-Domain Routing - Used to denote a range of IP addresses
- Egress - outbound
- Ingress - inbound

### Internet Gateway

### Router

### Route Tables

> A _route table_ contains a set of rules, called _routes_, that are used to determine where network traffic from your subnet or gateway is directed.

#### Key Terms

- **Main Route Table** - The route table that automatically comes with your VPC. It controls the routing for all subnets that are not explicitly associated with any other route table.
- **Custom Route Table** - A route table that you created for your VPC.
- **Edge Association** - A route table that you use to route _inbound_ VPC traffic to an appliance. You associate a route table with the internet gateway or virtual private gateway, and specify the network interface of your appliance as the target for VPC traffic.
- **Route Table Association** - The association between a route table and a subnet internet gateway, or virtual private gateway.
- **Subnet Route Table** - A route table that is associated with a subnet.
- **Gateway Route Table** - A route table that's associated with an internet gateway or virtual private gateway
- **Local Gateway Route Table** - A Route table that's associated with an Outposts local gateway.
- **Destination** - The destination CIDR where you want traffic to go. For example, an external corporate network with a 172.16.0.0/12 CIDR.
- **Target** - The target through which to send the destination traffic; for example, ann internet gateway.
- **Local route** - A default route for communication within the VPC.

#### How Route Tables work

Your VPC has an _implicit_ router, and you use route tables to control where traffic is directed. Each subnet in your VPC **must** be associated with a route table, which controls the routing for the subnet (subnet route table). You can explicitly associate a subnet with a particular route table. Otherwise, the subnet is implicitly associated with the main route table. A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same subnet route table.

#### Destinations and Targets Examples

- **Destination** - **Target** - **Note**
- `0.0.0.0/0` - `igw-xxx` - internet gateway
- `::/0` - `eigw-xxx` - egress-only internet gateway
- `10.0.0.0/16` - `Local` - IPv4
- `2001:db8:1234:1a00::/56` - `Local` - IPv6
- `172.31.0.0/16` - `pcx-xxx` - Peering connection

* The destination for the route `0.0.0.0/0` represents **all** IPv4 addresses. Its target is your Internet Gateway attached to your VPC. CIDR blocks for IPv4 and IPv6 are treated separately and you must create a route with access to IPv6 CIDR destinations if you want to IGW to access them.
* **Every route table contains a local route for you communication within the VPC. This route is added by default to all route tables.** If your VPC has more than one IPv4 CIDR block, your route table will contain a local route _for each_ IPv4 CIDR block. Same logic applies to IPv6 CIDR blocks. You **cannot modify or delete** these routes in a subnet route table or in the main route table.

#### Questions

- What is the function of a route table and what are its rules called?
- Define Main Route Table
- Define Custom Route Table
- Define Edge Association
- Define Route Table Association
- Define Subnet Route Table
- Define Gateway Route Table
- Define Local Gateway Route Table
- Define Destination
- Define Target
- Define Local Route
- Does a VPC have an implicit router?
- Does every subnet in a VPC have to be associated with a route table?
- How many route tables can a subnet be associated with at one time?
- Can multiple subnets be associated with the same route table?
- What is the _all_ IPv4 destination CIDR address?
- What is the _all_ IPv6 destination CIDR address?
- Do IPv4 and IPv6 addresses need to handled with separate routes?
- Do all route tables come with a default local route? What is its purpose?
- Will you have a local route for _each_ CIDR block in your VPC?
- Can you modify or delete local routes in the subnet route table?
- Can you modify or delete local routes in the main route table?

### Network ACL

> An _optional_ layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You may set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC.

#### ACL vs Security Groups

**Security Group**

- Operates at the instance level
- Supports allow rules only
- Stateful: Return traffic is **automically allowed**, regardless of rules
- Only applies to an instance if someone specifies initially or at a later period

**Network ACL**

- Operates at the subnet level
- Supports allow rules and deny rules
- Stateless: Return **traffic must be explicitly allowed** by rules
- Automatically applies to _all_ instances in the subnet, which provides a nice blanket in the event an instance is missed

### Subnets

> A VPC spans all the AZs in a region. After creating

#### Design

- When you create a subnet, you specify the CIDR block for the subnet, which is a subset of the VPC CIDR block. **Each Subnet must reside entirely within on AZ and cannot span zones**.
- Fun Fact: You can _optional_ assign a IPv6 CIDR block to your VPC and assign IPv6 CIDR blocks to your subnets.

### Security Group

### Questions

---

- What is a VPC?
- What is a VPC comprised of?
- What are the differences between a default VPC and a custom VPC?
- What is VPC Peering?
- Can you peer VPCs across AWS account?
- What configuration is peering handled in?
- What is transitive peering? Does AWS VPC support it?
- How many subnets can exist in an AZ?
- Network ACLs, Security groups. Which is stateful and which is statless?
