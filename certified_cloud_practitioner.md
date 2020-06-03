# AWS Certified Cloud Practitioner

## Table of Contents

- [FAQ](#faq)
- [About the Exam](#about-the-exam)
- [Cloud Concepts](#cloud-concepts)
- [AWS Global Infrastructure](#aws-global-infrastructure)
- [Hands On](#hands-on)
- [Billing and Pricing](#billing-and-pricing)
- [Technology Overview](#technology-overview)

---

### FAQ

#### Who is the CCP for?

- Learning AWS foundational knowledge
- Shows you've poked around and can use the AWS console
- Focuses on billing and business-centric concepts
- Commonly obtained by _sales_ and _management_ to help inform VPs or CEO reasons to utilize AWS

#### What value does the CCP hold?

- Not a gilded title
- Can help superficially increase your AWS certification count
- Not recognized as an important recertification for developers on resumes

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

### About the Exam

#### Exam Guide Link

https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf

#### Content Outline

Cloud Concepts - 28%
Security - 24%
Technology - 36%
Billing and Pricing - 12%

---

### Cloud Concepts

#### What is cloud computing?

cloud computing - the practice of using a network of remote servers hosted on the Internet to store, manage and process data, rather than a local server or a personal coputer

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

#### Six advantages and benefits of cloud computing

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

#### Types of Cloud Computing

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

#### What is cloud computing?

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

### AWS Global Infrastructure

#### Where does all this cloud computing run?

- 69 availabilty zones within 22 geographic regions
- AWS serves over a million active customers in more than 190 countries
- Regions: physical location in the world with multiple Availability Zones
- Availability Zones: one or more discrete data centers
- Edge Location: datacenter owned by a trusted partner of AWS

#### Regions

- A geographically _distinct_ location which has multiple datacenters (AZs).
- Every region is physically isolated from and independent of every other region in terms of location, power, water supply.
- Each region has at least 2 AZs.
- AWS largest region is US-EAST.
- New services almost always become available first in US-EAST.
- Not all services are available in all regions.
- US-EAST-1 is the region where you see all your billing information.

#### Availabilty Zones

- An AZ is a datacenter owned and operated by AWS.
- AZs are represented by a Region Code, followed by a letter identifier eg. `us-east-1a`.
- Distributing your instances across multiple AZs allows failover configuration for handling requests when one goes down.
- < 10ms latency between AZs

#### Edge Locations

- An edge location is a datacenter owned by a trusted partner of AWS which has a direction connection to the AWS network.
- These locations serve request sfor CloudFront and Route 53.

#### GovCloud Regions

- AWS GovCloud Regions allow customers to host sensitive Controlled Unclassified Information and other types of regulated workloads.
- GovCloud Regions are only operated by employees who are US citizens.

---

### Hands On

#### To set billing alarms

- CloudWatch, Alarms

#### Create individual IAM user

- Root account should not be used

#### Log in with Systems Manager

- Session manager

#### AMI (Amazon Machine Instance)

- In instance, Actions, Image, Create image

#### Auto Scaling Groups

- Guarantee one server is running

#### Elastic Load Balancer (ELB)

- Load Balancers, Create New Load Balancer, Application Load Balancer
- Need to be running in at least 2 AZs

#### Simple Storage Server (S3)

#### Cloudfront

- Used as a CDN
- Serve static content as fast as possible

#### Relational Database Service (RDS)

- Production ~\$600/month
- Dev/Test ~\$250/month
- Free (750 hours)

#### Lambda

---

### Billing and Pricing

#### Introduction to EC2 Pricing Models

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
- commit to EC2 over a 1 or 3 year term
- can resell unused reserved instances
- reduced pricing is based on Term X Class Offering X Payment Option
- Payment Options: All upfront, partial upfront, no upfront
- Class Offerings
  - Standard - up to 75% savings; cannot change RI attributes
  - Convertible - up to 54% savings; allows you to change RI attributes if greater or equal in value
  - Scheduled - you reserve instances for specific time periods eg. once a week for a few hours; savings may vary
- RIs can be shared between multiple accounts within an org
- unused RIs can be sold in the Reserved Instance Marketplace

**Dedicated (most expensive)**

- dedicated servers
- multi-tenant vs single tenant
- can be on-demand or reserved (up to 70% off)
- when you need a guarantee of isolate hardware (enterprise requirements)

#### Free Services

- IAM
- Amazon VPC
- Auto Scaling\*
- CloudFormation\*
- Elastic Beanstalk\*
- Opsworks\*
- Amplify\*
- Appysync\*
- Codestar\*
- Organizations & COonsolidated Billing
- AWS Cost Explorer

* May provision services which cost money

#### AWS Support Plans

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

#### AWS Marketplace

AWS Marketplace is a curated digital catalogue with thousands of software listings from independen software vendors.

Easily find, buy, test and deploy software that already runs on AWS.

The product can be free to use or can have associated charge.

The sales channel for ISVs and Consulting Partners allows you to sell your solutions to other AWS customers.

Products can be offered as:

- Amazon Machine Images (AMIs)
- AWS CloudFormation templates
- SaaS offerings
- Web ACL
- AWS WAF rules

#### AWS Trusted Advisor

Advises you on security, saving money, performance, service limits and fault tolerance

5 Categories:

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

#### Consolidated Billing

One bill for all of your accounts.
You can designate one master account that pays the charges of all other member accounts.
Use Cost Explorer to visualize usage for consolidated billing.

**Volume Discounts**

- The more you use, the more you save

**AWS Cost Explorer**

AWS Cost Explorer lets you visualize, understand and manage your AWS costs and usage over time.

- Use forecasting to get an idea of future costs
- See data at monthly or daily level
- Use filter or grouping functionalities

#### AWS Budgets

Plan your service usage, service costs and instance reservations

- think of it like a billing alarm on steroids
- first 2 budgets are free of charge
- each budget is \$0.02 per day; ~0.60 / month
- 20,000 budgets limit

#### TCO Calculator

The Total Cost of Ownership allows you to estimate how much you would save switching to AWS.

#### AWS Landing Zone

- Helps Enterprises quickly set-up a secure, AWS multi-account
- Provides you with a baseline environment to get started with a multi-account achitecture
- AVM (Account Vending Machine)
  - Automatically provisions and configure new accounts via Service Catalog Template
  - Uses Single Sign-on (SSO) for managing and accessing accounts

#### Resource Groups and Tagging

**Tags** are words of phrases that act as metadata for organizing your AWS

**Resource Groups** are a collection of resources that share one or more tags

Resource Groups can display details about a group of resource based on

- metrics
- alarms
- configuration settings

#### AWS Quickstart

Prebuilt templates by AWS and AWS Partners to help you deploy popular stacks on AWS.

A Quick Start is composed of 3 parts:

1. A reference architecture for the deployment
2. AWS CloudFormation templates that automate and configure the deployment
3. A deployment guide explaining the architecture and implementation in detail

#### AWS Cost and Usage Report

Generate a detailed spreadsheet, enabling you to better analyze and understand your AWS costs

- Places the reports into S3
- Use Athena to turn the report into a queryable database
- Use QuickSight to visualize your billing data as graphs

#### Organizations and Accounts

**Organizations** allow you to centrally manage billing, control access, compliance, security, and share resources

**Root Account User** is a single sign-in identity that has complete access to all AWS services and resources in an account
Each account has a Root Account User

**Organization Units** are a group of AWS accounts within an organization which can also contain other organizational units - creating a hierachy

**Service Control Policies** give central control over the alloed permissions for all accounts in your organization, helping to ensure your accounts stay within your organization's guidelines

### Technology Overview

#### AWS Networking

**Region** - the geographical location of the network
**AZ** - the data center of your AWS resources
**VPC** (virtual private cloud) - a logically isolated section of the AWS Cloud where you can launch AWS resources
**Internet Gateway** - enable access to the internet
**Route Tables** - determine where network traffic fom your subnets are directed
**NACLs** - acts as a firewall at the subnet level
**Security Groups** - acts as firewall at the instance level
**Subnets** - a logical partition of an IP network into multiple, smaller network segments

#### Database Services

**DynamoDB** - NoSQL key/value database (Cassandra-like)
**DocumentDB** - NoSQL Document database that is MongoDB compatible
**RDS** - Relational Database Service that supports multiple engines

- Engines: MySQL, PostGres, Maria DB, Oracle, Microsoft SQL Server, Aurora
- Aurora - 5x faster than MySQL and 3x faster than PSQL
- Aurora Serverless - only runs when you need it, like AWS
  Lambda

**Neptune** - Managed graph database
**Redshift** - Columnar database, petabyte warehouse

- 1000 TB = 1 PB

**ElastiCache** - Redis or Memcached database
