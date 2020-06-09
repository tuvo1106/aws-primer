# AWS Certified Cloud Practitioner

## Table of Contents

- [FAQ](#faq)
- [Exam Guide Overview](#exam-guide-overview)
- [S3](#s3)
- [AWS Snowball](#aws-snowball)
- [Virtual Private Cloud](#virtual-private-cloud)
- [Network Access Control List](#network-access-control-list)

---

## FAQ

#### Why get AWS Solutions Architect Associate?

- Finding creative solutions by leveraging cloud services instead of reinventing the wheel. Big picture thinking.
- Shows you have broad knowledge across many domains.
- Great for those who get bored easily since you need to wear multiple hats.
- It's less about the "how are we going to implement this? and more about the "what are we going to implement?
- Not uncommon to be part of business development team, might need to ban extrovert with charismatic speaking skills.

#### Who is the Solution Architect Associate for?

- Architectue Diagrams
- Constant Learning
- Pricing
- Security

#### What value does Solution Architect Associate hold?

- The _most popular_ AWS certification.
- In demand with startups because you can help wherever help is needed.
- Recognized as the _most important_ certification at the associate level.
- Will help you _stand out_ on resumes.
- _Not likely to increase your salary_ but more job opportunities.

#### Still not sure why?

- Most in-demand.
- Not too easy but not too hard.
- Requires least amount of technical knowledge.
- When in doubt which cert to take, since it provides most flexible learning path.
- If you're new to Cloud Computing, take the CCP and then Solution Architect Associate.

#### How long to study to pass Solution Architect Associate

- If you're a developer... 1 month of study.
- If you're a bootcamp grad... 1-2 months of study.
- If you're a cloud engineer... 20 hours of study.

#### How much, how long, how many questions?

- \$150
- 130 minutes
- 65 questions
- ~72% passing score
- Valid for 3 years

---

## Exam Guide Overview

- Design resilient architectures - 34%
  - Choose reliable/resilient storage.
  - Determine how to design decoupling mechanisms using AWS services.
  - Determine how to design a multi-tier achitectural.
    solution.
  - Determine how to design high availability and/or fault tolerant architecture.
- Design performant architectures - 24%
  - Choose performant storage and database.
  - Apply caching to improve performance.
  - Design solutions for elasticity and scalability.
- Specify secure applications and architectures - 26%
  - Determine how to secure application tiers.
  - Determine how to secure data.
  - Define the networking infrastructure for a single VPC application.
- Design cost-optimized architectures - 10%
  - Determine how to design cost-optimal storage.
  - Determine how to design cost-optimal compute.
- Define operationally-excellent architectures - 6%
  - Choose design features in solutions that enable operational resilience.

Whitepapers

Read _AWS Well-Achitected Framework_.
Read _Architecting for the Cloud: AWS Best Practices_.

---

## S3

#### Introduction to S3

- Object-based storage service.
- Serverless storage in the cloud.
- Don't worry about filesystems or disk space.

**What is Object Storage (Object-based Storage)?**

- data storage architecture that manages data as objects, _as opposed_ to other storage architectures:
  - file systems - manages data as files and file hierarchy.
  - block storage - manages data as blocks within sectors and tracks.

S3 provides you with unlimited storage. You do not need to think about the underlying infrastructure.
The S3 console provides an interface for you to uploaad and access your data.

##### S3 Object

Objects contain your data. They are like files.
Objects may consist of:

- Key - name of object.
- Value - the data itself made up of a sequence of bytes.
- Version ID - when versioning available, the version of object.
- Metadata - additional information attached to the object.

You can stre data from _0 Bytes_ to _5 Terabytes_ in size.

##### S3 Bucket

Buckets hold objects. Buckets can also have folders which in turn hold objects.
S3 is a a universal namespace so bucket names must be unique (think like having a domain name).

---

#### Storage Classes

Trade Retrieval Time, Accessibilty and Durability for Cheaper Storage.

```
11 9's = 99.99999999999
 9 9's = 99.999999999
```

|                Class                |                                                                                        Description                                                                                        |
| :---------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|         Standard (default)          |                                                      Fast! 99.99% availability, 11 9's durability, replicated across at least 3 AZs.                                                      |
|         Intelligent Tiering         | Uses ML to analyze your object usage and determine the appropriate storage class. Data is moved to the most cost-effective access tier, without any performance impact or added overhead. |
| Standard Infrequently Accessed (IA) |                    Still Fast! Cheaper if you access files less than once a month. Additional retrieval fee is applied. 50% less than standard (reduced availability).                    |
|             One Zone IA             |              Still Fast! Objects only exist in one AZ. Availability is 99.5% but cheaper than Standard IA by 20% less. Data could get destroyed. A retrieval fee is applied.              |
|               Glacier               |                                    For long-term storage cold storage. Retrieval of data can take minutes to hours but the off is very cheap storage.                                     |
|        Glacier Deep Archive         |                                                              The lowest cost storage class. Data retrieval time is 12 hours.                                                              |

**S3 Guarantees**

- Platform is built for 99.99% availability.
- Amazon gaurantees 99.9% availability.
- Amazon guarantees 11 9's of durability.

---

#### S3 Security

- All new buckets are **PRIVATE** when created by default.
- Logging per request can be turned on in a bucket. Log files are generated and saved in a different bucket (even a bucket in a different AWS account if desired).
- Access control is configured using **Bucket Policies** and **Access Control Lists (ACL)**.

---

#### S3 Encryption

**Encryption In Transit**

- Traffic between your local host and S3 is achieved via SSL/TLS.

**Server Side Encryption (SSE) - Encryption At Rest**

- Amazon helps you encrypt the object data.
- S3 Managed Keys - (Amazon manages all the keys).
- SSE-AES - S3 handles the key, uses AES-256 algorithm.
- SSE-KMS - Envelope encryption, AWS KMS and you manage the keys.
- SSE-C - Customer provided key (you manage the keys).

**Client-Side Encryption**

- You encrypt your own files before uploading them to S3.

---

#### Data Consistency

**New Objects (PUTS)**

- _Read After Write_ consistency.
- When you upload a new S3 object, you able to read immediately after writing.

**Overwrite (PUTS) or Delete Objects (DELETES)**

- _Eventual_ consistency.
- When you overwrite or delete an object, it takes time for S3 to replicate versions to AZs.
- If you read immediately, S3 may return you an old copy. You need to generally wait a few seconds before reading.

---

#### Cross Region Replication (CRR)

- When enabled, any object that is uploaded will be _automatically replicated_ to another region(s).
- Provides higher durability and potential disaster recovery for objects.
- You must have _versioning_ turned on both the _source_ and _destination_ buckets.
- You can have CRR replicate to another AWS account.

---

#### S3 Versioning

- Store all versions of an object in S3.
- Once enabled, it cannot be disabled, only suspended in bucket.
- Fully integrates with S3 Lifecycle rules.
- MFA Delete feature provides extra protection against deletion of your data.

---

#### S3 Lifecycle Management

- Automate the process of moving objects to different Storage classes or deleting objects all together.
- Can be used togethe with _versioning_.
- Can be applied to both _current_ and _previous_ versions.

---

#### Transfer Acceleration

- Fast and secure transfer of files _over long distances_ between your end users and an S3 bucket.
- Utilizes _CloudFront's_ distributed Edge Locations.
- Instead of uploading to your bucket, users use a _distinct URL_ for an Edge Location.
- As data arrives at the Edge Location it is automatically routed to S3 over a specially optimized network path(Amazon's backbone netowrk).

---

#### Presigned URLs

- Generate a URL which provides you temporary access to an object to either upload or download object data. Presigned URLs are commoonly used to _provide access to private objects_. You can use AWS CLI or AWS SDK to generate Presigned URLs.
- For example, you have a web app which needs to allow users to download files from a password-protected area. Your web app generates a presigned URL which expires after 5 seconds. The user downloads the file.

---

#### MFA Delete

- **MFA Delete** ensures users cannot delete objects from a bucket unless they provide their MFA code.
- MFA Delete can only be enabled under these conditions:
  - The _AWS CLI_ must be used to turn on MFA.
  - The bucket must have _versioning turned on_.

Only the bucket owner logged in as **Root User** can DELETE objects from bucket.

---

### AWS Snowball

- Petabyte-scale data transfer service.
- Move data onto AWS via physical briefcase computer.

#### Snowball

- Low Cost - it cost thousands of dollars to transfer 100TB over high speed internet. Snowball can reduce that costs by _1/5th_.
- Speed - It can take 100TB over 100 days to transfer over high speed internet. Snowball can reduce that transfer time by _less than a week_.
- Snowball features and limitations:
  - E-Ink display (shipping info).
  - Tamper and weather proof.
  - Data is encrypted end-to-end (256-bit encryption).
  - Uses Trusted Platform Module (TPM) - a specialized chip on an endpoint device that stores RSA encryption keys specific to the host system for hardware authentication.
  - For security purposes, data transfers must be completed within _90 days_.of the Snowball being prepared.
  - Snowball can Import and Export from S3.
- Snowballs come in 2 sizes:
  - 50 TB (42 TB of usable space)
  - 80 TB (72 TB of usable space)

---

#### Snowball Edge

- Petabyte-scale data transfer service.
- Move data onto AWS via physical briefcase computer.
- Move storage and on-site compute capabilities.

Similar to Snowball but with _more storage_ and with _local processing_.

Snowball Edge features and limitations:

- LCD diplay (shipping information and other functionality).
- Can undertake local processing and edge-computing workloads.
- Can use in a cluster in groups of 5 to 10 devices.
- Three options for device configurations:
  - Storage optimized (25 vCPUs)
  - Compute optimized (54 vCPUs)
  - GPU optimized (25 vCPUs)

Snowball Edge comes in 2 sizes:

- 100 TB (83 TB of usable space)
- 100 TB Clustered (45 TB per node)

---

#### Snowmobile

A _45-foot long_ ruggedized _shipping container_, pulled by a _semi-trailer truck_.
Transfer up to _100PB_ per Snowmobile, exabyte-scale migration.

AWS personnel will help you connect your network to the snowmobile and when data transfer is complete, they'll drive it back to AWS to import into S3 or Glacier.

Security Features

- GPS Tracking
- Alarm monitoring
- 24/7 video surveillance
- An escort security while in transit (optional)

---

#### Virtual Private Cloud

#### Introduction

Provision a _logically isolated section of the AWS cloud_ where you can launch AWS resources in a virtual network that you define.

---

#### Core Components

Think of a AWS VPC as your own _personal data center_.
Gives you complete control over your virtual networking environment.

![VPC](./images/vpc.png)

Combining these components and services is what makes up your VPC:

- Internet Gateway (IGW)
- Virtual Private Gateway (VPN Gateway)
- Routing Tables
- Network Access Control Lists (NACLs) - Stateless
- Security Groups (SG) - Stateful
- Public Subnets
- Private Subnets
- Nat Gateway
- Customer Gateway
- VPC Endpoints
- VPC Peering

---

#### Key Features

- VPCs are _Region Specific_; they do not span regions.
- You can create up to _5 VPC_ per region.
- Every region comes with a default VPC.
- You can have _200 subnets_ per VPC.
- You can use _IPv4 CIDR Block_ and in addition to a _IPv6 CIDR Blocks_ (the address of the VPC).
- Cost nothing: VPC's, Route Tables, NACLs, Internet Gateways, Security Groups and Subnets, VPC Peering
- Some things cost money: NAT Gateway, VPC Endpoints, VPN Gateway, Customer Gateway
- DNS hostnames (should our instance have domain name addresses)

---

#### Default VPC

AWS has a default VPC in every region so you can immediately deploy instances.

- Create a VPC with a size /16 IPv4 CIDR block (172.31.0.0/16)
- Create a size /20 default subnet in each AZ.
- Create an Internet Gateway and connect it to your default VPC.
- Create a default network access control list (NACL) and associate it with our default VPC.
- Associate the default DHCP options set for your AWS account with your default VPC.
- When you create a VPC, it automatically has a main route table.

---

#### Default Everywhere IP

- 0.0.0.0/0 is also known as default.
- It represents all possile IP addresses.
- When we specify 0.0.0.0/0 in our route table for IGW we are allowing internet access.
- When we specify 0.0.0.0/0 in our security groups inbound rules we are allowing all traffic from internet access our public resources.
- When you see 0.0.0.0/0, just think of giving access from anywhere on the internet.

---

#### VPC Peering

VPC Peering allows you to connect one VPC to another over a direct network route using private IP addresses.

- Instances on peered VPCs behave just like they are on the same network.
- Connect VPCs across same or different AWS accounts and regions.
- Peering uses a Star Configuration: 1 Central VPC - 4 other VPCs.
- No Transitive Peering (peering must take place directly between VPCs)
  - Needs a one to one connect to immediate VPC.
- No Overlapping CIDR Blocks.

---

#### Route Tables

- Route tables are used to determine where network traffic is directed.
- Each subnet in your VPC _must be associated_ with a route table.
- A subnet can only be associated with one route table at a time, but you associate multiple subnets with the same route table.

---

#### Internet Gateway (IGW)

- The IGW allows your VPC access to the internet.
- The IGW does 2 things:
  - provide a target in your VPC route tables for internet-routable traffic.
  - perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.
- To route out to the internet, you need to add in your route tables for the IGW and set the destination to 0.0.0.0/0.

---

#### Bastion/Jumpbox

Bastions are EC2 instances which are security harden. They are designed to help you gain access to your EC2 instances via SSH or RCP that are in a _private subnet_.

They are also known as Jump boxes because you are jumping from one box to access another.

NAT Gateways/Instances are only intended for EC2 instances to gain outbound access to the internet for things such as security updates. NATs cannot/should not be used as Bastions.

System Manager's Sessions Manager replaces the need for Bastions.

---

#### Direct Connect

AWS Direct Connect is the AWS solution for establishing dedicated network connections from on-premises locations to AWS.

- Very fast network (lower bandwidth 50M - 500M or higher bandwidth (1GB or 10GB))
- Helps reduce network costs and increase bandwich thoughput (great for high traffic networks)
- Provides a more consistent network experience than a typical internet-based connection (reliable and secure)

---

#### VPC Endpoints

Think of a secret tunnel where you don't have to leave the AWS network.

VPC Endpoints allow you to _privately connect your VPC to other AWS services_.

- Eliminates the need for an Intnet Gateway, NAT device, VPN connection, or AWS Direct Connect connections.
- Instances in the VPC do not require a public IP address to communicate with service resources.
- Traffic between your VPC and other services _does not leave the AWS network_.
- Horizontally scaled, redundant and highly available VPC component.
- Allows secure communication between instances and services - without adding availaility risks or bandwidth constraints on your traffic.

There are 2 Types of VPC Endpoints:

- Interface Endpoints
- Gateway Endpoints

---

#### Interface Endpoints

Interface Endpoints are Elastic Network Interfaces (ENI) with a private IP address. They serve as an entry point for traffic going to a supported service.

Interface Endpoints are powered by AWS PrivateLink.

Pricing per VPC endpoint per AZ ($/hour) 0.01
Pricing per GB data processed ($) 0.01
~7.5/mo

---

#### Gateway Endpoints

A Gateway Endpoint is a gateway that is a target for a specific route in your route table, used for traffic destined for a supported AWS service.

- VPC GE's are free!
- To create a Gateway Endpoint, you must specify the VPC in which you want to create the endpoint, and the service to which you want to establish the connection.
- AWS Gateway Endpoint currently only supports 2 services: S3 and DynamoDB

#### VPC Flow Logs Introduction

VPC Flow Logs allow you to capture IP traffic information in-and-out of Network Interfaces within your VPC.

Flow Logs can be created for:

- VPC
- Subnets
- Network Interface

All log data is stored and accesible using Amazon CloudWatch Logs or S3.

---

#### VPC Flow Logs Log Breakdown

- Version
- Account ID
- Interface ID
- Source IPv4 or IPv6 addresses
- Destination IPv4 or IPv6 addresses
- Source port
- Destination port
- Protocol
- Packets
- Bytes
- Start - time in UNIX
- End - time in UNIX
- Action - ACCEPT or REJECT
- log-status - OK, NODATA, SKIPDATA

---

#### VPC Flow Logs Cheatsheet

- VPC Flow Logs cannot be tagged like other AWS resources.
- You cannot change the configuration of a flow after it's created.
- You cannot enable flow logs for VPCs which are peered with your VPC unless it is in the same account.
- Some instance traffic is not monitored:
  - Instance traffic generated by contacting the AWS DNS servers.
  - Windows license activation traffic from instances.
  - Traffic to and from the instance metadata address (169.254.169.254).
  - DHCP Traffic.

---

### Network Access Control List (NACLs)
