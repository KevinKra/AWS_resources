## EC2 Quiz (WIP)

> Content also includes material on EBS and EFS.

https://aws.amazon.com/ec2/faqs/

### Questions

#### EC2

- **Explain EC2.**

  > Elastic Compute Cloud is an AWS service that allows developers to provision compute resources on the Amazon cloud. You are able to provision and configure capacity with minimal friction. It provides complete control of your computing resources and the time required to obtain and boot new server instances takes mere minutes allowing you to scale capacity, both up and down, rapidly as your computing requirements change.

- **What does EC2 Allow developers to do now that they couldn't before?**

  > EC2 allows small development teams with limited capital the means to acquire massive compute resources with the means of dynamically reacting to unexpected spikes in load traffic. The service allows any developer to leverage Amazon's economy of scale with no required up-front costs or performance compromises. Developers are now free to innovate knowing that no matter how successful their businesses become, it will be inexpensive and simple to ensure they have the compute capacity they need to meet their business requirements.

- **What is the difference between using the local instance store and Amazon Elastic Block Store (EBS) for the root device?**

  > When you launch your EC2 instances you have the option to store your root device data on either the local instance store or on EBS. Storing your data on EBS allows your data to persist independently from the instance. If you shut down your instance your EBS will persist and can be used once more on restart or stand up.

  > The local instance store _only_ persists during the life of the instance. This is an inexpensive way to launch instances where data is not stored on the root device.

- **How long does it take for an instance to start running?**

  > Generally less than 10 minutes. This is dependent on many factors including the size of your AMI, the number of instances launching, and whether the AMI is being launched for the first time or not.

- **Is Amazon EC2 used in conjunction with Amazon S3?**

> Yes, Amazon EC2 is used jointly with Amazon S3 for instances with root devices backed by local instance storage. In order to execute systems in the Amazon EC2 environment, developers use the tools provided to load their AMIs into Amazon S3 and to move them between Amazon S3 and Amazon EC2.

- **Are is there a limit to how many EC2 instances I can run?**

> Yes. There is a limit on the number of running On-Demand Instances per AWS account per Region. On-Demand Instance limits are managed in terms of the number of virtual central processing units (vCPUs) that your running On-Demand Instances are using, regardless of the instance type.

- **What metric is now being used to determine and limit EC2 resources?**

> vCPU-based limits. You are limited to running one or more On-Demand Instances in an AWS account, and Amazon EC2 measures usage towards each limit based on the total number of vCPUs (virtual central processing unit) that are assigned to the running On-Demand instances in your AWS account.

- **What are the Default vCPU limits per family and how are they determined.**

> Running On-Demand Standard (A, C, D, H, I, M, R, T, Z) instances has a default vCPU limit of 1152 vCPUs across instances of the family. F, G, Inf, P, X are all limited to a default of 128 vCPUs.

- **Are On-Demand Instance vCPU-based limits regional?**

> Yes. On-Demand instance limits for AWS regions are set on a per-region basis.

- **Can these limits be increased?**

> EC2 automatically increases your On-Demand instances based on your usage. You can also request limit increases.

- **What does your Amazon EC2 Service Level Agreement guarantee?**

> A Monthly Uptime Percentage of at least 99.99% for Amazon EC2 and Amazon EBS within a Region.

- **How many different instance price models are there and what are their details?**

* **How many types of reserved instances exist and what are their details?**

* **What are the EC2 types and their respective use cases?**

* **Is termination protection on or off by default?**

* **On an EBS-backed instance, is the default action to delete the root EBS volume when the instance is deleted?**

* **Can the EBS Root Volumes of your DEFAULT AMI's be encrypted?**

* **Can additional EC2 instance volumes be encrypted?**

* **Which EC2 volume is the device OS installed onto?**

* **If you make a rule change to a security group, how quickly does it take affect?**

* **What happens if you delete an outbound rule in an EC2 instance?**

* **Can you blacklist ports or IP addresses with security groups?**

* **Can you attach more than one security group to an EC2 instance?**

* !!!

- **Are SGs stateful or stateless, what does this mean?**

- **Are NACLs stateful or stateless, what does this mean?**

- **Can you block specific IP addresses with SGs?**

* **Where are EBS snapshots saved? What does it mean that they are incremental?**

* **Can you take an EBS snapshot of your root volume? What should you do beforehand?**

* **Do EBS volumes have to be in the same AZ as their EC2 instance counterpart?**

* **What steps must you take in order to migrate an EC2 Instance from one _AZ_ to another?**

* **What steps must you take in order to migrate an EC2 Instance from one _Region_ to another?**

* **Are snapshots of encrypted volumes automatically encrypted themselves?**

* **Are volumes restored from encrypted snapshots encrypted automatically?**

* **Can you share encrypted snapshots?**

* **If you want to share a snapshot with other AWS accounts or make it public, what must you do?**

* **Can Root Volumes be encrypted?**

* **Can originally un-encrypted root volumes be encrypted?**

* **What is an Instance Store Volume (ISV) and how does it differ from EBS?**

* **What is Ephemeral Storage?**

* **Can Instance Store Volumes be stopped, can EBS volumes be stopped?**

* **Can either ISV or EBS volumes installed on root devices be saved if the underlying EC2 instance is terminated?**

* **What is CloudWatch used for?**

* **What is the default increment monitoring setting for CloudWatch with EC2?**

* **What is the overview difference between CloudWatch and CloudTrail?**

* **Does CloudWatch or CloudTrail monitor API calls in the AWS environment?**

* **CloudWatch can create Dashboards, events, and logs. What do these features do?**

* **What is EFS?**

* **What are Placement Groups?**

* **What are the three types of placement groups?**

* **Describe Clustered Placement Groups.**

* **Describe Spread Placement Groups.**

* **Describe Partitioned Placement Groups.**

* **Which placement groups can span multiple AZs, which Placement Group is confined to one AZ?**

* **Are there any restrictions to which EC2 instance types can be placed into placement groups?**

* **Does AWS recommend homogenous or heterogenous instances within clustered placement groups?**

* **Can you merge placement groups?**

* **Can you move an existing EC2 instance into placement group? What is a solution?**

* **What are the four EC2 pricing models?**

* **Describe the On Demand pricing model.**

* **Describe the Reserved pricing model.**

* **Describe the Spot pricing model.**

* **Describe the Dedicated Host pricing model.**

* **Describe Standard Reserved Instances.**

* **Describe Convertible Reserved Instances.**

* **Describe Scheduled Reserved Instances.**
