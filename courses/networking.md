## VPC overview

> A virtual data center in the cloud

- ex: EC2 instances are deployed into our default VPC. Everyone region in the world has a default VPC.

```
// General Implementation
Internet Gateway(IGW)/Virtual Private Gateway(VPG) => Router => Route Table => Network ACL => Public/Private Subnet + (Security Group + Instance)
```

#### What can you do with a VPC

- Launch instances into a subnet of your choosing.
- Assign custom IP address ranges in each subnet.
- Configure route tables between subnets.
- Create internet gateway and attach it to your VPC.
- Much better security control over AWS resources.
- Instance security groups.
- Subnet network Access Control Lists (ACLs.)

#### Default VPC vs Custom VPC

- Amazon provisions an default VPC in every region.
- Default VPC always has a default CIDR block with a 16-subnet mask - 172.31.0.0/16 .
- Default VPC is user friendly, allowing you to immediately deploy instances for testing purposes.
- Custom VPC allows you to tighten down security settings.
- All subnets in default VPC have a route to the internet, no private subnets in default VPCs.
- Each EC2 instance has a both public and private IP address.

#### VPC Peering

- Allows VPCs to connect to another via direct network route using private IP addresses, _as long as they're in the same region_.
- Instances behave as if they were on the same private network.
- You can peer VPCs with other AWS accounts as well as the same account.
- Peering is int a star configuration. 1 central VPC peers w/ 4 others. **NO TRANSITIVE PEERING**.
- Transitive Peering: One VPC cannot connect to the link of it's link. The link must be direct.
- VPCs without overlapping CIDRs _cannot_ be paired.
- If you delete the default VPC you have to called AWS to restore it.

#### Exam Tips

- VPC consists of IGWs/VPGs, Route Tables, Network Access Control Lists, Subnets, and Security Groups
- 1 Subnet = 1 AZ
- Security Groups are Stateful
- Network ACLs are stateless
- No transitive peering

---

## Connectivity

#### Private IP Address

Private IP addresses are not reachable over the internet. Rather, they are used for communication between instances in the same network. When you launch a new instance, it is given a private IP address and an internal DNS hostname that resolves to the private IP address of the instance.

#### Public IP Address

Public IP addresses are reachable over the internet. They can be used between for communication between instances and the internet. Each instance that is given a public IP address is given an _external_ DNS hostname. Public IP addresses are associated with your instances from the Amazon Public Pool of addresses. When you stop or terminate your instance your public IP address is released and a new one is assigned when your instance starts. If you want to retain your public IP address through these operations you need to use an **Elastic IP Address**.

#### Elastic IP Address

- Elastic IP Addresses are static or persistent public IP addresses that are allocated to your account and can be associated with instances as you require. They can be disassociated with your account when no longer needed. They will incur a charge while being reserved but not actually used.

---

## VPC Components

### Global Terms

- **CIDR block** - Classless Inter-Domain Routing - Used to denote a range of IP addresses
- Egress - outbound
- Ingress - inbound

### Internet Gateway

> An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows for communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.

- You can only attach **one IGW per VPC**.

#### Connecting EC2 Instances to the Internet

1. IGW must be connected to the VPC.
2. All instances in your subnet must have either a public IP address or an elastic IP address.
3. Ensure subnet's route table points to the internet gateway.
4. All NACL and Security Groups must be configured to allow the required traffic to and from your instance.

### Router

### Route Tables

> A _route table_ contains a set of rules, called _routes_, that are used to determine where network traffic from your subnet or gateway is directed.

- Each subnet in your VPC must be associated with a route table; the table controls routing for the subnet. A subnet can only be associated with one route table at a time, but you can associated multiple subnets with the same route table.

- Every VPC has a default root table and its good practice to leave it in its original state. Instead of changing the default root table, create a new root table to customize the network traffic associated with your vpc.

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

### NAT Device - Network Address Translation Device

> Use to connect EC2 instances in private subnets to connect to the internet or other AWS services, _but_ prevents the internet from initiating connections with instances within the private subnet.

- Private Subnet database instance may need internet access or the ability to connect to other AWS services.
- Forwards traffic from your private subnet to the internet or AWS services and returns the response back to the instances.
- When traffic goes to the internet the source IP address of your instance is replaced by the NAT device address and when the traffic comes back, the NAT device translates the address to your instance's private ID address.
- **NAT devices have to be in a public subnet so they get internet connectivity.**

#### NAT Gateway vs NAT instance

AWS provides two kinds of NAT devices. AWS recommends the NAT gateway because its a managed service with better availability and bandwidth than instances. Each NAT Gateway is created in a specific AZ with redundancy in that zone.

- NAT Instance is launched from a NAT AMI and runs as an instance in your VPC. Requires extra management and legwork.

- **NAT Gateways require an Elastic IP Address.**
- Once created you need to update your root table associated w/ private subnet to point internet bound traffic to the NAT Gateway.

### VGW - Virtual Private Gateway

- The VPN concentrator on the AWS side of a hybrid network solution. It connects _via a VPN connection_ to customer networks via a **Customer Gateway** that exists on their resources.

* A VPC spans all the AZs in a region, a subnet is _always_ mapped to a single AZ.
* The netmask for your VPC's default subnet is always 20, which provides 4096 addresses.
* _NO_ subnets are automatically created when a VPC is created.
* You _cannot_ launch instances in a VPC **unless** their are subnets in your VPC.

### Subnets

A range of IP addresses in your VPC. A public subnet is used for resources that must be connected to the internet and a private subnet is used for resources that won't be connected to the internet.

#### Public Subnets

- Public subnets are _made_ public because the main Route Table sends the Public Subnet's traffic, that is destined for the internet, to the Internet Gateway.

#### Private Subnets

- Protects resources that don't need connection to the internet or you want to protect from the internet, for example Databases instances.

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
