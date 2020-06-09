# Quiz Questions

---

1. Which of the below are components that can be configured in the VPC section of th AWS management console? (choose 2)

- a. EBS volumes
- b. Endpoints
- c. DNS records
- d. Subnet
- e. Elastic Load Balancer

**Answer** - B, D

EBS volumes and ELB must be configured in EC2 section.
DNS must be configured in Amazon Route 53.

---

2. What statement is true in relation to data stored within an AWS Region?
- a. Data is always replicated to another region
- b. Data is not replicated outside of a region unless you configure it
- c. Data is always automatically replicated to at least one another AZ
- d. Data is automatically archived after 90 days

**Answer** - B

---

3. Which type of storage stores objects comprised of key, value pairs?
- a. Amazon EFS
- b. Amazon EBS
- c. Amazon S3
- d. Amazon DynamoDB

**Answer** - C

Amazon S3 is an object-based storage system that stores objects that are comprised of key, value pairs.
Amazon DynamoDB stores items, not objects, based on key, value pairs.
Amazon EBS is a block-based storage system.
Amazon EFS is a file-based storage system.

---

4. Which of the facts below are accurate in relation to AWS Regions? (choose 2)
- a. Each region consists of a collection of VPCs
- b. Regions are Content Delivery Network (CDN) endpoints for CloudFront
- c. Each region consists of 2 or more availability zones
- d. Regions have direct, low-latency, high throughput and redudant network connections between each other
- e. Each region is designed to be completely isolate from the other Amazon Regions

**Answer** - C, E

A region is not a collection of VPCs, it is composed of at least 2 AZs. VPCs exist within accounts on a per region basis.
AZs (not regions) have direct, low-latency, high throughput and redundant network connections between each other.
Edge locations (not regions) are Content Delivery Network (CDN) endpoints for CloudFront.

---

5. Which of the following would be good reasons to move from on-premises to the AWS Cloud? (choose 2)
- a. Outsource all security responsibility
- b. Gain access to free technical support services
- c. Reduce costs through easier right-sizing of workloads
- d. Improve agility and elasticity
- e. Gain end-to-end operational management of the entire infrastructure stack

**Answer** - C, D

AWS offers elastic computing with the ability to adjust workloads, monitor utilization and programatically make changes. You can improve agility and elasticity through services such as Auto Scaling, ELB and highly scalable services such as S3 and Lambda.
You do not get free technical services with AWS or end-to-end operational management of the entire infrastructure stack.
You are still responsible for ensuring the security of your application, users and data.

---

6. Which AWS program can help an organization to design, build, and manage their workload?
- a. AWS Business Development Manager
- b. APN Consulting Partners
- c. APN Technology Consultants
- d. AWS Technical Account Manager

**Answer** - B

APN Consulting Partners are professional services firms that help customers of all sizes design, architect, build, migrate and manage their workloads and applications. Consulting partners include System Integrators (SIs), Strategic Consultancies, Agencies, Managed Service Providers (MSPs), and Value-Added Resellers (VARs).

---

7. An Amazon EC2 instance running the Amazon Linux 2 AMI is billed in what increment?
- a. Per hour
- b. Per CPU
- c. Per GB
- d. Per second

**Answer** - D

EC2 instances are billed in one second increments, with a minimum of 60 seconds.
You do pay for _EBS_ on a per GB of provisioned storage basis.

---

8. Which AWS service lets you add user sign up, sign-in and access control to web and mobile apps?
- a. AWS CloudHSM
- b. AWS Artifact
- c. AWS Directory Service
- d. AWS Cognito

**Answer** - D

Amazon Cognito scales to millions of users and supports sign-in with social identity providers.
AWS Directory Service enables your directory-aware workloads.
AWS Artifact is your go-to, central resource for compliance-related information that matters to you.
AWS CloudHSM is a cloud-based hardware security module that enables you to easily generate and use your own encryption keys on the AWS cloud.

---

9. Which aspects of security on AWS are customer responsibilties? (choose 2)
   a. Availability of AWS regions
   b. Server-side encryption
   c. Physical acess controls
   d. Setting up account password policies
   e. Patching of storage systems

**Answer** - B, D

AWS is responsible for the "security of the cloud". This includes protecting the infrastructure such as hardware, software, networking and facilities that run AWS Cloud services.
The customer is responsible for "security in the cloud". This includes IAM (Identity and Access Management), encryption of data, protection of network traffic and operating system, and firewall configuration.

---

10. How does AWS assist organizations' with their capacity requirements?
- a. With AWS you don't pay for data centres
- b. With AWS you only pay for what you use
- c. You don't own the infrastructure
- d. You don't need to guess your capacity needs

**Answer** - D

All these statements are true, but the question is asking about capacity, i.e. how organizations ensure they don't over or under-provision their resources.
The ability to scale on demand is a key advantage of AWS.

---

11. Which AWS services can be utilized at no cost? (choose 2)
- a. Identify and Access Management (IAM)
- b. Amazon VPC
- c. Amazon S3
- d. Amazon CloudFront
- e. Amazon RedShift

**Answer** - A, B

The only services that do not incur cost in this list are IAM and VPC

---

12. Which AWS support plan comes with a Technical Account MAnager (TAM)?
- a. Enterprise
- b. Business
- c. Basic
- d. Developer

**Answer** - A

Only the Enterprise plan comes with a TAM

---

13. Which AWS services are used for analytics? (choose 2)
- a. Amazon Athena
- b. Amazon EMR
- c. Amazon ElastiCache
- d. Amazon S3
- e. Amazon RDS

**Answer** - A, B

Amazon Elastic Map Reduce (EMR) provides a managed Hadoop framework that makes it easy, fast, and cost-effective to process vast amoutns of data across dyunamically scalable Amazon EC2 instance
Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL
ElastiCache is a data caching service that is used to help improve the speed/performance of web applications running on AWS
Amazon RDS is Amazon's relational database and is primarily used for transactional workloads
Amazon S3 is used for object storage

---

14. Which service allows you to automatically expand and shrink your application in response to demand?
- a. Amazon DynamoDB
- b. AWS ElastiCache
- c. AWS Auto Scaling
- d. Amazon Elastic Load Balancing

**Answer** - C

Auto Scaling automatically responds to demand by adding or removing EX2 instances to ensure the right amount of compute capacity is available at any time
Amazon ELB distributes incoming requests to EC2 instances. It can be used in conjunction with Auto Scaling
AWS ElastiCache provides in-memory cache and database services
Amazon DynamoDB is a NoSQL database

---

15. With which service can a developer upload code form a Git repository and have the service handle the end-to-end deployment of the resources?
- a. AWS CodeCommit
- b. Amazon ECS
- c. AWS Elastic Beanstalk
- d. AWS CodeDeploy

**Answer** - C

AWS Elastic Beanstalk can be used to quickly deploy and manage applications in the AWS Cloud. Developers upload applications and Elastic Beanstalk dandles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring
AWS CodeCommit is a fully-managed source control service that hosts secure Git-based respositories
AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Lambda, and your on-premises servers
Amazon Elastic Container Service is a managed services for running Docker containers

---

16. Under the shared responsibility model, what are examples of shared controls? (choose 2)
- a. Sotrage system patching
- b. Patch management
- c. Service and Communications Protection
- d. Configuration management
- e. Physical and environmental

**Answer** - B, D

Shared Controls- Controls which apply to both the infrastructure layer and customer layers, but in completely separate contexts or perspectives
**Patch Management**- AWS is responsible for patching and fixing flaws within the infrastructure, but customers are responsible for patching their gues OS and applications
**Configuration Management**- AWS maintains the configuration of its infrastructure devices, but a customer is responsible for configuring their own guest operating systems, databases, and applications
Service and Communications Protection is an example of a customer specific control
Storage system patching is an AWS responsibility

---

17. Which service allows an organization to view operational data from multiple AWS services through a unified user interface and automate operational tasks?
- a. AWS Config
- b. AWS CloudWatch
- c. AWS Systems Manager
- d. AWS OpsWorks

**Answer** - C

AWS Systems Manager give you visibility and control of your infrastructure on AWS. Systems Manager provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources
AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet
AWS Config is a fully-managed service that provides you with an AWS resource inventory, configuration history, and configuration change notifications tro enable security and regulatory compliance
Amazon CloudWatch is a monitoring service for AWS cloud resources and the applications you run on AWS. You use CloudWatch for perforamnce monitoring, not auttomating operational tasks

---

18. What are two ways that moving to an AWS cloud can benefit an organization? (choose 2)
- a. Switch to a CAPEX model
- b. Increase speed and agility
- c. Stop guessing about capacity
- d. Gain greater control of data center security
- e. Depreciate assets over a longer timeframe

**Answer** - B, C

Eliminate guessing on your infrastructure capactity needs. When you make a capacity decision prior to deploying an application, yuou often end uip either sitting on expensive idle resources or dealing with limited capacity. With cloud computing, these problems go away. You can access as much or as little capacity as you need, and scale up and down as required with only a few minutes' notice
In a cloud computing environtment, new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes. This results in a dramatic incrase in agility for the organization, since the cost of deployment and develop is significantly lower
Cloud is based on an operational (POEX) model, not a capital expenditure (CAPEX) model
Cloud does not provide the ability to depreciate assets over a longer timeframe as you generally do not own the assets

---

19. Which architectural best practice aims to reduce the interdependencies between services?
- a. Removing Single Points of Failure
- b. Loose Coupling
- c. Services, Not Servers
- d. Automation

**Answer** - B

As application complexity increases, a desirable attribute of an IT system is that it can be broken into smaller, loosely coupled components. This means that IT systems should be designed in a way that reduces interdependencies-a change or a failure in one component should not cascade to other components
The concept of loose coupling includes "well-defined interfaces" which reduce interdependencies in a system by enabling interaction only through specific, technology-agnostic interfaces (e.g. RESTful APIs)

---

20. Which if the statements below is correct in relation to Consolidated Billing? (choose 3)
- a. You can combine usage and share volume pricing discounts
- b. You pay a fee per linked account
- c. You receive one bill per AWS account
- d. You are not charged a fee
- e. You receive a single bill for multiple accounts

**Answer** - A, D, E

Consolidated billing has the following benefits:
- One bill - You can get one bill for multiple accounts
- Easy tracking - You can track the charges across multiple accounts and download the combined cost and usage data
- Combined usage - You can combine the usage across all accounts in the organization to share the vulume pricing discount between these accounts. This can result in a lower charge for your project, department, or company than with individual standalone accounts
- No extra fee - Consolidated billing is offered at no additional cost

---
