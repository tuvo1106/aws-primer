# AWS Certified Cloud Practitioner

## Table of Contents

- [FAQ](#faq)
- [About the Exam](#about-the-exam)
- [Cloud Concepts](#cloud-concepts)
  - [What is Cloud Computing?](#what-is-cloud-computing)
  - [Six advantages and benefits of cloud computing](#six-advantages-and-benefits-of-cloud-computing)
  - [Types of Cloud Computing](#types-of-cloud-computing)
  - [Cloud Computing Models](#cloud-computing-models)
- [AWS Global Infrastructure](#aws-global-infrastructure)
  - [Where does all this cloud computing run?](#where-does-all-this-cloud-computing-run)
  - [Regions](#regions)
  - [Availability Zones](#availability-zones)
  - [Edge Locations](#edge-locations)
  - [GovCloud Regions](#govcloud-regions)
- [Billing and Pricing](#billing-and-pricing)
  - [Introduction to EC2 Pricing Models](#introduction-to-ec2-pricing-models)
  - [Free Services](#free-services)
  - [AWS Support Plans](#aws-support-plans)
  - [AWS Marketplace](#aws-marketplace)
  - [AWS Trusted Advisor](#aws-trusted-advisor)
  - [Consolidated Billing](#consolidated-billing)
  - [AWS Budgets](#aws-budgets)
  - [TCO Calculator](#tco-calculator)
  - [AWS Landing Zone](#aws-landing-zone)
  - [Resource Groups and Tagging](#resource-groups-and-tagging)
  - [AWS Quickstart](#aws-quickstart)
  - [AWS Cost and Usage Report](#aws-cost-and-usage-report)
  - [Organizations and Accounts](#organizations-and-accounts)
- [Technology Overview](#technology-overview)
  - [AWS Networking](#aws-networking)
  - [Database Services](#database-services)
  - [Provisioning](#provisioning)
  - [Computing Services](#computing-services)
  - [Storage Services](#storage-services)
  - [Business Centric Services](#business-centric-services)
  - [Enterprise Integration](#enterprise-integration)
  - [Logging Services](#logging-services)
  - [Know your Initialisms](#know-your-initialisms)
- [Security](#security)
  - [Shared Responsibility Model](#shared-responsibility-model)
  - [AWS Compliance programs](#aws-compliance-programs)
  - [AWS Artifact](#aws-artifact)
  - [Amazon Inspector](#amazon-inspector)
  - [AWS WAF](#aws-waf)
  - [AWS Shield](#aws-shield)
  - [Penetration Testing](#penetration-testing)
  - [Guard Duty](#guard-duty)
  - [Key Management Service](#key-management-service)
  - [Amazon Macie](#amazon-macie)
  - [Security Groups vs NACLs](#security-groups-vs-nacls)
  - [AWS VPN](#aws-vpn)
- [Variation](#variation-study)
  - [Cloud Services](#cloud-services)
  - [Connect Service](#connect-service)
  - [Elastic Transcoder vs MediaConvert](#elastic-transcoder-vs-mediaconvert)
  - [SNS vs SQS](#sns-vs-sqs)
  - [Amazon Inspector vs AWS Trusted Advisor](#amazon-inspector-vs-aws-trusted-advisor)
  - [ALB vs NLB vs CLB](#alb-vs-nlb-vs-clb)
  - [SNS vs SES](#sns-vs-ses)
  - [AWS Artifact vs AWS Inspector](#aws-artifact-vs-aws-inspector)

---

## FAQ

#### Who is the CCP for?

- Learning AWS foundational knowledge
- Shows you've poked around and can use the AWS console
- Focuses on billing and business-centric concepts
- Commonly obtained by _sales_ and _management_ to help inform VPs or CEO reasons to utilize AWS

#### What value does the CCP hold?

- Not a gilded title
- Can help superficially increase your AWS certification count
- Not recognized as an important certification for developers on resumes

#### Thinking of skipping the CCP? Think again...

- It's an easy win, and a confidence booster
- Mitigate unknown conditions that cause stress or distraction for future exam
- Directly prepare for the Solution Architect Associate

#### How long to study to pass CCP?

- If you're a developer... 8 hours
- If you're a bootcamp grad... 15 hours
- If you're sales or management... 20 hours

#### Where to take test?

- PSI
- Pearson VUE

#### Cost/Logistics

- \$100
- 90 minutes
- 65 questions
- 70% passing score
- Valid for 3 years

---

## About the Exam

#### Exam Guide Link

https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf

---

#### Content Outline

- Cloud Concepts - 28%
- Security - 24%
- Technology - 36%
- Billing and Pricing - 12%

---

## Cloud Concepts

#### _What is Cloud Computing?_

The practice of using a network of remote servers hosted on the Internet to store, manage and process data, rather than a local server or a personal computer

**On-premise**

- you own the servers
- you hire the IT people
- you pay or rent the real estate
- you take all the risk

**Cloud-providers**

- someone else owns the servers
- someone else hires the IT people
- someone else pays or rents the real estate
- you are responsible for your configuring cloud services and code, someone else takes care of the rest

---

#### _Six advantages and benefits of cloud computing_

**Trade capital expense for variable expense**

- No upfront-cost
- Pay on-demand

**Benefit from massive economies of scale**

- You are sharing the cost with other customers

**Stop guessing capacity**

- Instead of paying for idle or underutilized servers, you can scale up or down to meet needs

**Increase speed and agility**

**Stop spending money on running and maintaining data centers**

- Focus on customers, rather than the heavy lifting of racking, stacking and powering servers

**Go global in minutes**

---

#### _Types of Cloud Computing_

**SaaS**

- for customers
- a complete product that is run and managed by the service provider
- Gmail, Salesforce, Office365

**PaaS**

- for developers
- removes the need for your organization to manage the underlying infrastructure so you can focus on the deployment and management of your applications
- Elastic Beanstalk, Heroku

**IaaS**

- for admins
- the basic building blocks for cloud IT; provides access to networking features, computers and data storage space
- AWS, GCP, Azure

---

#### _Cloud Computing Models_

**Cloud**

- Squarespace, Dropbox
- Startups, new projects and companies

**Hybrid**

- Deloitte
- Using cloud and on-prem
- Banks, FinTech, Legacy on-prem

**On-Premise**

- "Private cloud"
- Public sector eg. government
- Super sensitive data eg. hospitals
- Large enterprise with heavy regulation eg. insurance companies

---

## AWS Global Infrastructure

#### _Where does all this cloud computing run?_

- 69 availability zones within 22 geographic regions
- AWS serves over a million active customers in more than 190 countries
- Regions: physical location in the world with multiple Availability Zones
- Availability Zones: one or more discrete data centers
- Edge Location: datacenter owned by a trusted partner of AWS

---

#### _Regions_

- A geographically _distinct_ location which has multiple datacenters (AZs).
- Every region is physically isolated from and independent of every other region in terms of location, power, water supply.
- Each region has at least 2 AZs.
- AWS largest region is US-EAST.
- New services almost always become available first in US-EAST.
- Not all services are available in all regions.
- US-EAST-1 is the region where you see all your billing information.

---

#### _Availability Zones_

- An AZ is a datacenter owned and operated by AWS.
- AZs are represented by a Region Code, followed by a letter identifier eg. `us-east-1a`.
- Distributing your instances across multiple AZs allows failover configuration for handling requests when one goes down.
- < 10ms latency between AZs

---

#### _Edge Locations_

- An edge location is a datacenter owned by a trusted partner of AWS which has a direction connection to the AWS network.
- These locations serve requests for CloudFront and Route 53.

---

#### _GovCloud Regions_

- AWS GovCloud Regions allow customers to host sensitive Controlled Unclassified Information and other types of regulated workloads.
- GovCloud Regions are only operated by employees who are US citizens.

---

## Billing and Pricing

#### _Introduction to EC2 Pricing Models_

**On-Demand (Least Commitment)**

- default
- low cost and flexible
- only pay her hour
- short-term, spiky, unpredictable workloads
- cannot be interrupted
- for first time apps

**Spot (up to 90% off; biggest savings)**

- request spare computing capacity
- flexible start and end times
- can handle interruptions (server randomly stopping and starting)
- for non-critical background jobs
- AWS Batch is an easy and convenient way to use Spot Pricing
- instances can be terminated by AWS at any time
- if your instance is terminated, you don't get charged for a partial hour of usage
- if YOU terminate an instance, you will still be charged

**Reserved Instances (up to 75% off; best long-term)**

- steady state or predictable usage
- can resell unused reserved instances
- RIs can be shared between multiple accounts within an org
- unused RIs can be sold in the Reserved Instance Marketplace
- reduced pricing is based on Term X Class Offering X Payment Option

**Term**

- 1 Year
- 3 Years

**Class Offerings**

- Standard - up to 75% savings; cannot change RI attributes
- Convertible - up to 54% savings; allows you to change RI attributes if greater or equal in value
- Scheduled - you reserve instances for specific time periods eg. once a week for a few hours; savings may vary

**Payment Options**

- All upfront
- Partial upfront
- No upfront

**Dedicated (most expensive)**

- dedicated servers
- multi-tenant vs single tenant
- can be on-demand or reserved (up to 70% off)
- when you need a guarantee of isolate hardware (enterprise requirements)

---

#### _Free Services_

- IAM
- Amazon VPC
- Auto Scaling\*
- CloudFormation\*
- Elastic Beanstalk\*
- Opsworks\*
- Amplify\*
- Appysync\*
- Codestar\*
- Organizations & Consolidated Billing
- AWS Cost Explorer

\* May provision services which cost money

---

#### _AWS Support Plans_

**Basic**

- \$0 / month
- 7 Trusted Advisor Checks

**Developer**

- \$20 / month
- Tech support via email ~24 hours until reply
- No third party support
- 7 Trusted Advisor Checks

**Business**

- \$100 / month
- Tech support via email ~24 hours until reply
- Tech support via chat/phone anytime 24/7
- ALL Trusted Advisor Checks

**Enterprise**

- Tech support via email ~24 hours until reply
- Tech support via chat/phone anytime 24/7
- Personal Concierge
- TAM (Technical Account Manager)
- \$15,000 / month
- ALL Trusted Advisor Checks

---

#### _AWS Marketplace_

AWS Marketplace is a curated digital catalogue with thousands of software listings from independent software vendors.

- Easily find, buy, test and deploy software that already runs on AWS.
- The product can be free to use or can have associated charge.
- The sales channel for ISVs and Consulting Partners allows you to sell your solutions to other AWS customers.

Products can be offered as:

- Amazon Machine Images (AMIs)
- AWS CloudFormation templates
- SaaS offerings
- Web ACL
- AWS WAF rules

---

#### _AWS Trusted Advisor_

Advises you on security, saving money, performance, service limits and fault tolerance.

**Cost Optimization**

- Idle Load Balancers
- Unassociated Elastic IP Addresses

**Performance**

- High Utilization EC2 Instances

**Security**

- MFA on Root Account
- IAM Access Key Rotation

**Fault Tolerance**

- Amazon RDS Backups

**Service Limits**

- VPC

---

#### _Consolidated Billing_

One bill for all of your accounts.
You can designate one master account that pays the charges of all other member accounts.
Use Cost Explorer to visualize usage for consolidated billing.

**Volume Discounts**

- The more you use, the more you save

**AWS Cost Explorer** lets you visualize, understand and manage your AWS costs and usage over time.

- Use forecasting to get an idea of future costs
- See data at monthly or daily level
- Use filter or grouping functionalities

---

#### _AWS Budgets_

Plan your service usage, service costs and instance reservations

- think of it like a billing alarm on steroids
- first 2 budgets are free of charge
- each budget is \$0.02 per day; ~0.60 / month
- 20,000 budgets limit

---

#### _TCO Calculator_

The Total Cost of Ownership allows you to estimate how much you would save switching to AWS.

---

#### _AWS Landing Zone_

- Helps Enterprises quickly set-up a secure, AWS multi-account
- Provides you with a baseline environment to get started with a multi-account architecture
- AVM (Account Vending Machine)
  - Automatically provisions and configure new accounts via Service Catalog Template
  - Uses Single Sign-on (SSO) for managing and accessing accounts

---

#### _Resource Groups and Tagging_

**Tags** are words of phrases that act as metadata for organizing your AWS

**Resource Groups** are a collection of resources that share one or more tags. Resource Groups can display details about a group of resource based on:

- metrics
- alarms
- configuration settings

---

#### _AWS Quickstart_

Prebuilt templates by AWS and AWS Partners to help you deploy popular stacks on AWS.

A Quick Start is composed of 3 parts:

1. A reference architecture for the deployment
2. AWS CloudFormation templates that automate and configure the deployment
3. A deployment guide explaining the architecture and implementation in detail

---

#### _AWS Cost and Usage Report_

Generate a detailed spreadsheet, enabling you to better analyze and understand your AWS costs

- Places the reports into S3
- Use Athena to turn the report into a queryable database
- Use QuickSight to visualize your billing data as graphs

---

#### _Organizations and Accounts_

- **Organizations** allow you to centrally manage billing, control access, compliance, security, and share resources
- **Root Account User** is a single sign-in identity that has complete access to all AWS services and resources in an account. Each account has a Root Account User
- **Organization Units** are a group of AWS accounts within an organization which can also contain other organizational units - creating a hierarchy
- **Service Control Policies** give central control over the allowed permissions for all accounts in your organization, helping to ensure your accounts stay within your organization's guidelines

---

## Technology Overview

#### _AWS Networking_

- **Region** - the geographical location of the network
- **AZ** - the data center of your AWS resources
- **VPC** (virtual private cloud) - a logically isolated section of the AWS Cloud where you can launch AWS resources
- **Internet Gateway** - enable access to the internet
- **Route Tables** - determine where network traffic fom your subnets are directed
- **NACLs** (network access control list) - acts as a firewall at the subnet level
- **Security Groups** - acts as firewall at the instance level
- **Subnets** - a logical partition of an IP network into multiple, smaller network segments

---

#### _Database Services_

- **DynamoDB** - NoSQL key/value database (Cassandra-like)
- **DocumentDB** - NoSQL Document database that is MongoDB compatible
- **RDS** - Relational Database Service that supports multiple engines
  - Engines: MySQL, PostGres, Maria DB, Oracle, Microsoft SQL Server, Aurora
  - Aurora - 5x faster than MySQL and 3x faster than PSQL
  - Aurora Serverless - only runs when you need it, like AWS Lambda
- **Neptune** - Managed graph database
- **Redshift** - Columnar database, petabyte warehouse
  - 1000 TB = 1 PB
- **ElastiCache** - Redis or Memcached database

---

#### _Provisioning_

The allocation or creation of resources and services to a customer.

- **Elastic Beanstalk** - service for deploying and scaling web applications and services developed with Java, .NET, Python... (Heroku-like)
- **OpsWorks** - configuration management service that provides managed instances of Chef and Puppet
- **CloudFormation** - infrastructure as code, JSON or YAML
- **AWS Quickstart** - pre-made packages that can launch and configure your AWS compute, network, storage, and other services required to deploy a workload on AWS
- **AWS Marketplace** - a curated digital catalogue with thousands of software listings from independent software vendors.

---

#### _Computing Services_

- **EC2** - Elastic Compute Cloud, highly configurable server eg. CPU, Memory, Network, OS

All services below are running EC2s under the hood

- **ECS** - Elastic Container Service, Docker as a Service. Highly scalable, high performance container orchestration service that supports Docker containers, pay for EC2 instances
- **Fargate** - Microservices where you don't think about the infrastructure. Pay per task
- **EKS** - Kubernetes as a Service. Easy to deploy, manage, and scale containerized applications using Kubernetes
- **Lambda** - serverless functions. Run code without provisioning or manage servers. You only pay for the compute time you consume.
- **Elastic Beanstalk** - orchestrates various AWS services, including EC2, S3, Simple Notification Service (SNS), CloudWatch, autoscaling, and ELB
- **AWS Batch** - plans, schedules, and executes your batch computing workloads across the full range of AWS compute services and features, such as EC2 and Spot instances

---

#### _Storage Services_

- **S3** - Simple Storage Service - object storage
- **S3 Glacier** - low cost storage for archiving and long-term backup
- **Storage Gateway** - hybrid cloud storage with local caching
  - File Gateway, Volume Gateway, Tape Gateway
- **EBS** - Elastic Block Storage - hard drive in the cloud you can attach to EC2 instances
  - SSD, HHD
- **EFS** - file storage mountable to multiple EC2 instances at the same time
- **Snowball** - physically migrate lots of data via a computer suitcase 50-80 TB
  - Snowball Edge - a better version (100 TB)
  - Snowmobile - Shipping container, pulled by a semi-trailer truck (100PB)

---

#### _Business Centric Services_

- **Amazon Connect** - Call Center. Cloud-based call center service you can setup in just a few clicks - based on the same proven system used by the Amazon customer service teams.
- **Workspaces** - Virtual Remote Desktop - Secure managed service for provisioning either Windows or Linux desktops
- **WorkDocs** - A content creation and collaboration service - easily create, edit and share content saved centrally in AWS (Sharepoint)
- **Chime** - AWS Platform for online meetings, video conferencing, and business calling
- **WorkMail** - Managed business email, contacts and calendar service
- **Pinpoint** - marketing campaign management system you can use for sending targeted email, SMS, push notifications, and voice messages
- **SES** - Simple Email Service. A cloud-based email sending service designed for marketers and application developers to send marketing, emails
- **QuickSight** - a Business Intelligence (BI) service. Connect multiple datasources and quickly visualize data

---

#### _Enterprise Integration_

Going Hybrid!

- **Direct Connect** - dedicated gigabit network connection from your premises to AWS. Imagine having a direct fibre optic cable running straight to AWS
- **VPN** - establish a secure connection to your AWS network
  - Site-to-site VPN - connecting your on-premise to your AWS network
  - Client VPN - connecting a client to your AWS network
- **Storage Gateway** - a hybrid storage service that enables your on-premise applications to use AWS cloud storage. You can use this for backup and archiving, disaster recovery, cloud data processing, storage tiering, and migration
- **Active Directory** - enables your directory-aware workloads

---

#### _Logging Services_

- **CloudTrail** - logs all API calls between AWS services
  - detect developer misconfiguration
  - detect malicious actors
  - automate responses
- **CloudWatch** - a collection of multiple services
  - CloudWatch Logs, Metrics, Events, Alarms, Dashboard

---

#### _Know your Initialisms_

- **IAM** - Identify and Access Management
- **S3** - Simple Storage Service
- **SWF** - Simple Workflow Service
- **SNS** - Simple Notification Service
- **SQS** - Simple Queue Service
- **SES** - Simple Email Service
- **SSM** - Simple Systems Manager
- **RDS** - Relational Database Service
- **VPC** - Virtual Private Cloud
- **VPN** - Virtual Private Network
- **CFN** - CloudFormation
- **WAF** - Web Application Firewall
- **MQ** - Amazon ActiveMQ
- **ASG** - Auto ScalingGroups
- **TAM** - Technical Account Manager
- **ELB** - Elastic Load Balancer
- **ALB** - Application Load Balancer
- **NLB** - Network Load Balancer
- **EC2** - Elastic Cloud Compute
- **ECS** - Elastic Container Service
- **ECR** - Elastic Container Repository
- **EBS** - Elastic Block Storage
- **EFS** - Elastic File Storage
- **EMR** - Elastic MapReduce
- **EB** - Elastic Beanstalk
- **ES** - Elasticsearch
- **EKS** - Elastic **Kubernetes** Service
- **MKS** - Managed **Kafka** Service
- **IoT** - Internet of Things
- **RI** - Reserved Instances

---

## Security

#### _Shared Responsibility Model_

- **IN** - Customers are responsible for Security **in** the Cloud
  - Data Configuration
- **OF** - AWS is responsible for Security **of** the Cloud

  - Hardware
  - Operation of Managed Services
  - Global Infrastructure

**Detailed Breakdown**

- **Customer**
  - Customer Data
  - Platforms, Applications, Identity and Access Management (IAM)
  - Operating System, Network and Firewall Configuration
  - Client-Side Data Encryption and Data Integrity Authentication
  - Server-Side Encryption (File System and/or Data)
  - Network Traffic Protection (Encryption, Integrity, Identity)
- **AWS**
  - Software
  - Compute
  - Storage
  - Database
  - Networking
  - Hardware/AWS Global Infrastructure
  - Region
  - Availability Zones
  - Edge Locations

---

#### _AWS Compliance programs_

**Compliance Programs**
Examples

- Health Insurance Portability and Accountability Act (HIPAA)
  - US Legislation that provides data privacy and security provisions for safeguarding medical information.
- The Payment Card Industry Data Security Standard (PCI DSS)
  - Standard for when you want to sell things online and you need to handle credit card information.

---

#### _AWS Artifact_

- No cost, self-service portal for on-demand access to AWS' compliance reports
- Checks are based on global compliance frameworks
- Reports will be in Adobe Acrobat Reader (Other PDF readers are not supported)

---

#### _Amazon Inspector_

- **Hardening** - The act of eliminating as many security risks possible

- AWS Inspector runs a security benchmark again specific EC2 instances.
- Can perform both **Network** and **Host** Assessments
  - Install the AWS agent on your EC2 instances
  - Run an assessment for your assessment target
  - Review your findings and remediate security issues

_CIS benchmark has 699 checks_

---

#### _AWS WAF_

- AWS Web Application Firewall protect your web applications from common web exploits
- Write your own `rules` to ALLOW or DENY traffic based on the contents of an HTTP requests
- Use a `ruleset` from a trusted AWS Security Partner in the AWS WAF Rules Marketplace
- WAF can be attached to either **CloudFront** or an **Application Load Balancer**

Protects web applications covered in **OWASP Top 10** most dangerous attacks:

- Injection
- Broken Authentication
- Sensitive data exposure
- XML External Entities (XXE)
- Broken Access control
- SEcurity misconfigurations
- Cross Site Scripting (XSS)
- Insecure Deserialization
- Using Components with known vulnerabilities
- Insufficient logging and monitoring

---

#### _AWS Shield_

AWS Shield is a **managed** DDoS (Distributed Denial of Service) protection service that safeguards applications running on AWS

**What is DDoS**?

- A malicious attempt to disrupt normal traffic by flooding a website with a large amount of fake traffic

- All AWS customers benefit from the automatic protections of AWS Shield Standard, at no additional charge
- AWS Shield Standard is applied to traffic through **Route53** or **CloudFront**
- Protects from **Layer 3, 4 and 7** attacks
  - 7 Application
  - 4 Transport
  - 3 Network

**Shield Standard** - Free

- For protection against most common DDoS attacks
- Access to tools and best practices to build a DDoS resilient architecture
- Automatically available on all AWS Services

**Shield Advanced** - \$3000/year

- For additional protection against larger and more sophisticated attacks
- visibility into attacks
- 24/7 access to DDoS experts for complex cases
- Available on:
  - Amazon Route 53
  - Amazon CloudFront
  - Elastic Load Balancing
  - AWS Global Accelerator
  - Elastic IP (Amazon Elastic Compute Cloud and Network Load Balancer)

---

#### _Penetration Testing_

- An authorized simulated cyberattack on a computer system performed to evaluate the security of the system.

Can you perform PenTesting on AWS? **Yes**

- **Permitted Services**

  - EC2 instances, NAT Gateways, and ELD
  - RDS
  - CloudFront
  - Aurora
  - API Gateways
  - AWS Lambda and Lambda@Edge functions
  - Lightsail resources
  - Elastic Beanstalk environments

- **Prohibited Activities**

  - DNS zone walking via Amazon Route 53 Hosted Zones
  - Denial of Service (DoS), Distributed Denial of Service (DDoS), Simulated DoS, Simulated DDoS
  - Port flooding
  - Protocol flooding
  - Request flooding (login request flooding, API request flooding)

_Other Simulated Events will need an approval by AWS_

---

#### _Guard Duty_

**IDS/IPS** - Intrusion Detection System and Intrusion Protection System

**Guard Duty** - A threat detection service that continuously monitors for malicious, suspicious activity and unauthorized behavior. It uses Machine Learning to analyze the AWS logs:

- CloudTrail logs
- VPC Flow logs
- DNS logs

_It will alert you of **Findings** which you can automate an incident response via CloudWatch Events or 3rd party services_

---

#### _Key Management Service_

A managed service that makes it easy for you to create and control the encryption keys used to encrypt your data

- KMS is a multi-tenant HSM (hardware security module)
- Many AWS services are integrated to use KMS to encrypt your data with a simple checkbox
- KMS uses Envelope Encryption

**Envelope Encryption**

- When you encrypt your data key with a master key as an additional layer of security.

---

#### _Amazon Macie_

Macie is a fully managed service that continuously monitors **S3 data access** activity for anomalies, and generates detailed alerts when it detects risk of unauthorized access or inadvertent data leaks.

_Macie works by using Machine Learning to Analyze your CloudTrail logs_

- Macie Alerts
  - Anonymized Access
  - Config Compliance
  - Credential Loss
  - File Hosting
  - Identity Enumeration
  - Information Loss
  - Location Anomaly
  - Open Permissions
  - Privilege Escalation
  - Ransomware
  - Service Disruption
  - Suspicious Access

Macie will identify your most at-risk users which could lead to a compromise.

---

#### _Security Groups vs NACLs_

**Security Groups**

- Acts as a firewall at the **instance** level
- Implicitly denies all traffic
- You create Allow rules

_Eg. Allow an EC2 instance to access on port 22 for SSH_

**NACLs** - Network Access Control Lists

- Acts as a firewall at the subnet level
- You create Allow and Deny rules

_Eg. Block a specific IP address known for abuse_

---

#### _AWS VPN_

**VPN** lets you establish a secure and **private tunnel** from your network or device to the AWS global network

**AWS Site-to-Site VPN**

- Securely connect on-premises networks or branch office site to VPC

**AWS Client VPN**

- Securely connect users to AWS or on-premise networks

---

## Variation Study

#### _Cloud\* Services_

- **CloudFormation**
  - Infrastructure as code, set up services via templating script eg. yml, json
- **CloudTrail**
  - logs all _api calls_ between _aws services_ (who we can blame)
- **CloudFront**
  - Content Distribution Network, it creates a cached copy of your website and copies to servers located near people trying to download your website
- **CloudWatch** - a collection of multiple services
  - CloudWatch Logs - any custom log data, Memory usage, Rails logs, NGINX logs
  - CloudWatch Metrics - metrics that are based off of logs eg. Memory usage
  - CloudWatch Events - triggers an event based on conditions eg.
  - CloudWatch Alarms - triggers notifications based on metrics
  - CloudWatch Dashboard - create visualizations based on metrics
- **CloudSearch**
  - Search engine, you have an e-commerce website and you want to add a search bar

---

#### _\*Connect Service_

- **Direct Connect** - Dedicated Fiber Optics Connection from datacenter to AWS
- **Amazon Connect** - Call center service
- **Media Connect** - new version of Elastic Transcoder, converts videos to different video types

---

#### Elastic Transcoder vs MediaConvert

Both services transcodes videos

- **Elastic Transcoder** - the old way. Transcodes videos to streaming formats.
- **AWS Elemental MediaConvert** - the new way. Transcodes videos to streaming formats. Overlays images, inserts video clips, extracts caption data, robust UI

---

#### SNS vs SQS

They both connect apps via messages.

- **Simple Notification Service** - pass along messages

  - send notifications to subscribers of topics via multiple protocol eg. HTTP, email, SQS, SMS
  - SNS is generally used for sending _plain text emails_ which is triggered via other AWS services. The best example of this is billing alarms.
  - Can retry sending in case of failure for HTTPS
  - Really good for webhooks, simple internal emails, triggering lambda functions

- **Simple Queue Service** - queue up messages, guaranteed delivery eg. PubSub (publisher-subscriber model)
  - places messages into a queue. Applications pull queue using AWS SDK
  - Can retain message for up to 14 days.
  - Can send them in sequential order or in parallel
  - Can ensure only one message is sent
  - Can ensure messages are delivered at least once
  - Really good for delayed tasks, queueing up emails

---

#### Amazon Inspector vs AWS Trusted Advisor

Both are security tools and they perform audits

- **Amazon Inspector**

  - audits a single EC2 instance that you've selected
  - Generates a report from a long list of security checks i.e. 699 checks

- **Trusted Advisor**
  - Trusted Advisor does not generate out a PDF report
  - Gives you a holistic view of recommendations across multiple services and best practices

---

#### ALB vs NLB vs CLB

All load balancers

- **Application**
  - Layer 7 requests
  - HTTP and HTTPS traffic
  - Routing rules, more usability from one load balancer
  - Can attack WAF
- **Network**
  - Layer 4 IP protocol data
  - TCP and TLS traffic where extreme performance is required
  - Capable of handling millions of requests per second while maintaining ultra-low latencies
  - Optimized for sudden and volatile traffic patterns while using a single static IP address per AZ
- **Classic** (old)
  - Layer 4 and Layer 7
  - Intended for applications that were built withing the EC2-classic network
  - Does not target groups

---

#### SNS vs SES

- **Simple Notification Service** - practical and internal

  - send notifications to subscribers of topics via multiple protocol eg. HTTP, email, SQS, SMS
  - SNS is generally used for sending _plain text emails_ which is triggered via other AWS services. The best example of this is billing alarms.
  - Most exam questions are going to be talking about SNS because lots of services trigger SNS for notifications
  - You need to know what are _topics_ and _subscriptions_

- **Simple Email Service** - professional, marketing, emails
  - a cloud-based email service e.g. SendGrid
  - SES sends html emails, SNS cannot
  - SES receives inbound emails
  - SES can create Email Templates
  - Custom domain name email
  - Monitor your email reputation

---

#### AWS Artifact vs AWS Inspector

Both Artifact and Inspector compile out PDFs

- **AWS Artifact**

  - Why should an enterprise trust AWS?
  - Generates a security report that's based on global compliance frameworks sch as:
    - Service Organization Control (SOC)
    - Payment Card Industry (PCI)

- **Amazon Inspector**
  - How do we know this EC2 instance is secure? Prove it?
  - Runs a script that analyzes your EC2 instance, then generates a PDF report telling you which security checks passed.
  - Audit tool for security of EC2 instances
