# AWS Developer - Associate

## Table of Contents

- [FAQ](#faq)
- [Exam Guide Overview](#exam-guide-overview)


---

## FAQ

#### Who is the Developer Associate for?

- Web Developers who are looking to add **Cloud Computing** skills to part of the their developer toolkit
- Think about how to build **Cloud-First** web-applications to push complexity into managed cloud services
- How to deploy web-applications for a variety of cloud architectures
- Transitioning from a Web Developer role into a Cloud Engineer role

#### What Value does the Developer Associate Hold?

- The Hardest Associate AWS Certification
- Practical Knowledge that will help you do the job of a **Cloud Engineer**
- Will help you stand out on resumes, although not likely to increase your salary

#### How long to study to pass the Developer Associate

- If you are a developer
  - 1.5 months of study
- If you are a bootcamp grad
  - 2 months of study
- If you are a Cloud Engineer
  - 30 hours of study
  
#### Details about the test
  
- Cost $150
- Takes 130 minutes
- 65 Questions
- ~72% for a passing score
- Valid for 3 years
  
## Exam Guide

#### Exam Breakdown

- Course Code: DVA-C01
- Passing grade 720/1000
- There are 65 Questions
  - You can afford to get 18 questions wrong
- Duration 130 mins (2 mins per question)
- Two types of questions
  - Multiple choice (Choose 1 out of 4)
  - Multiple response (Choose 2 or more out of 5 or more)
- Breakdown
  - 22% Deployment (14~15 questions)
  - 26% Security (16~17 questioins)
  - 30% Development with AWS Services (19~20 questions)
  - 10% Refactoring (6~7 questions)
  - 12% Monitoring and Troubleshooting (7~8 questions)
  
#### Recommended Whitepapers

- **Architecting for the Cloud: AWS Best Practices (Oct 2018)**
- **Practicing Continuous Integration and Continuous Delivery on AWS Accelerating Software Delivery with DevOps (June 2017)**
- Microservices on AWS (Sept 2017)
- Serverless Architectures with AWS Lambda (Nov 2017)
- Optimizing Enterprise Economics with Serverless Architectures (Apr 2019)
- Running Containerized Microservices on AWS (Nov 2017)
- Blue/Green Deployments on AWS (Aug 2016)

 ---
 
 ## Elastic Beanstalk
 
 Quickly deploy and manage web-apps on AWS
 
 #### Introduction
 
- What is Platform as a Service? (PaaS)
  - A platform allowing customers to develop, run, and manage applications without the complexity of building and maintaining the infrastructure typically associated with developing and launching an app.

- Choose a platform, upload your code and it runs with little knowledge of the infrastructure.
  - Not recommended for **Production** for Enterprise level applications

- Elastic Beanstalk is powered by a CloudFormation teamplate:
  - Elastic Load Balancer
  - Autoscaling Groups
  - RDS Database
  - Monitoring (CloudWatch, SNS)
  - In-Place and Blue/Green deployment methodologies
  - Security (Rotates passwords)
  - Can run Dockerized environments
  
#### Supported Languages

- Generic
  - Docker
  - Multi-container Docker
- Preconfigured
  - Elastic Beanstalk Packer Builder
  - Go
  - .NET (Windows/IIS)
  - Java
  - Node.js
  - Ruby
  - PHP
  - Python
  - Tomcat
- Preconfigured - Docker
  - GlassFish
  - Go
  - Python
  
#### Web vs Worker Environment

