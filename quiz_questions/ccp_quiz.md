# Quiz Questions

---

1. Which of the below are components that can be configured in the VPC section of th AWS management console? (choose 2)
   a. EBS volumes
   b. Endpoints
   c. DNS records
   d. Subnet
   e. Elastic Load Balancer

**Answer** - B, D

EBS volumes and ELB must be configured in EC2 section.
DNS must be configured in Amazon Route 53.

---

2. What statement is true in relation to data stored within an AWS Region?
   a. Data is always replicated to another region
   b. Data is not replicated outside of a region unless you configure it
   c. Data is always automatically replicated to at least one another AZ
   d. Data is automatically archived after 90 days

**Answer** - B

---

3. Which type of storage stores objects comprised of key, value pairs?
   a. Amazon EFS
   b. Amazon EBS
   c. Amazon S3
   d. Amazon DynamoDB

**Answer** - C

Amazon S3 is an object-based storage system that stores objects that are comprised of key, value pairs.
Amazon DynamoDB stores items, not objects, based on key, value pairs.
Amazon EBS is a block-based storage system.
Amazon EFS is a file-based storage system.

---

4. Which of the facts below are accurate in relation to AWS Regions? (choose 2)
   a. Each region consists of a collection of VPCs
   b. Regions are Content Delivery Network (CDN) endpoints for CloudFront
   c. Each region consists of 2 or more availability zones
   d. Regions have direct, low-latency, high throughput and redudant network connections between each other
   e. Each region is designed to be completely isolate from the other Amazon Regions

**Answer** - C, E

A region is not a collection of VPCs, it is composed of at least 2 AZs. VPCs exist within accounts on a per region basis.
AZs (not regions) have direct, low-latency, high throughput and redundant network connections between each other.
Edge locations (not regions) are Content Delivery Network (CDN) endpoints for CloudFront.

---

5. Which of the following would be good reasons to move from on-premises to the AWS Cloud? (choose 2)
   a. Outsource all security responsibility
   b. Gain access to free technical support services
   c. Reduce costs through easier right-sizing of workloads
   d. Improve agility and elasticity
   e. Gain end-to-end operational management of the entire infrastructure stack

**Answer** - C, D

AWS offers elastic computing with the ability to adjust workloads, monitor utilization and programatically make changes. You can improve agility and elasticity through services such as Auto Scaling, ELB and highly scalable services such as S3 and Lambda.
You do not get free technical services with AWS or end-to-end operational management of the entire infrastructure stack.
You are still responsible for ensuring the security of your application, users and data.

---

6. Which AWS program can help an organization to design, build, and manage their workload?
   a. AWS Business Development Manager
   b. APN Consulting Partners
   c. APN Technology Consultants
   d. AWS Technical Account Manager

**Answer** - B

APN Consulting Partners are professional services firms that help customers of all sizes design, architect, build, migrate and manage their workloads and applications. Consulting partners include System Integrators (SIs), Strategic Consultancies, Agencies, Managed Service Providers (MSPs), and Value-Added Resellers (VARs).

---

7. An Amazon EC2 instance running the Amazon Linux 2 AMI is billed in what increment?
   a. Per hour
   b. Per CPU
   c. Per GB
   d. Per second

**Answer** - D

EC2 instances are billed in one second increments, with a minimum of 60 seconds.
You do pay for _EBS_ on a per GB of provisioned storage basis.

---

8. Which AWS service lets you add user sign up, sign-in and access control to web and mobile apps?
   a. AWS CloudHSM
   b. AWS Artifact
   c. AWS Directory Service
   d. AWS Cognito

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
    a. With AWS you don't pay for data centres
    b. With AWS you only pay for what you use
    c. You don't own the infrastructure
    d. You don't need to guess your capacity needs

**Answer** - D

All these statements are true, but the question is asking about capacity, i.e. how organizations ensure they don't over or under-provision their resources.
The ability to scale on demand is a key advantage of AWS.

---
