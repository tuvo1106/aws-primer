# AWS Developer - Associate

## Table of Contents

- [FAQ](#faq)
- [Exam Guide Overview](#exam-guide-overview)
  - [Exam Breakdown](#exam-breakdown)
  - [Recommended Whitepapers](#recommended-whitepapers)
- [Elastic Beanstalk](#elastic_beanstalk)
  - [Introduction](#introduction)
  - [Supported Languages](#supported-languages)
  - [Web vs Worker Environment](#web-vs-worker-environment)
  - [Web Environments](#web-environments)
  - [Deployment Policies](#deployment-policies)
  - [All At Once Deployment](#all-at-once-deployment)
  - [Rolling](#rolling)
  - [Rolling with Additional Batch](#rolling-with-additional-batch)
  - [Immutable](#immutable)
  - [EB - Deployment Methods](#eb-deployment-methods)
  - [In-Place vs Blue/Green Deployment](#in-place-vs-blue/green-deployment)
  - [Configuration Files](#configuration-files)
  - [Env Manifest](#env-manifest)
  - [Linux Server Configuration](#linux-server-configuration)
  - [EB CLI](#eb-cli)
  - [Configuration RDS](#configuration-rds)
  - [Elastic Beanstalk Cheat Sheet](#elastic-beanstalk-cheat-sheet)



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
  
## Exam Guide Overview

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

![Web vs Worker Environments](./images/eb_web_vs_worker_env.png)

- Web Environment
  - Create an Auto Scaling Group
  - **Creates an Elastic Load Balancer**
- Worker Environment
  - Creates an Auto Scaling Group (ASG)
  - Creates an SQS Queue
  - Installs the Sqsd daemon on the EC2 instances
  - Creates CloudWatch Alarm to dynamically scale instances based on health
 
#### Web Environments

![Web Environments](./images/eb_web_env.png)

- Load Balanced Environment
  - Uses Auto Scaling Groups and set to scale
  - Uses and ELB
  - Designed to Scale
- Single-Instance Environment
  - Still uses an ASG but Desired Capacity set to 1 to ensure server is always running
  - No ELD to save on cost
  - Public IP Address has to be used to route traffic to server

#### Deployment Policies

- These are the Deployment Policies available with Elastic Beanstalk


| Deployment Policy        | Load Balanced Env           | Single Instance Env  |
| ------------- |:-------------:| -----:|
| All at once      | True | False |
| Rolling      | True      |   False |
| Rolling with additional batch | True      |    False |
| Immutable | True      |    True |

*Rolling and Rolling with additional batch unavailable in Single Instance env because you need an Elastic Load Balancer*

#### All At Once Deployment

1. Deploys the new app version to all instances at the same time
2. Takes all instances **out of service** while the deployment processes
3. Servers become available again

The **fastest** but most **dangerous** method
**In case of failure**
- You need to roll back the changes by re-deploying the original version again to all instances

#### Rolling

1. Deploys the new app version to a batch of instances at a time
2. Takes the batch's insntances **out of service** while the deployment process
3. Reattaches updated instances
4. Goes onto next batch, taking them out of service
5. Reattaches those instances (rinse and repeat)

#### Rolling with Additional Batch

1. Launch new instance thjat will be used to replace a batch
2. Deploy update app versiont to new batch
3. Attach the new batch and terminate the existing batch

Rolling with Addtional Batch's ensure our capacity is never reduced. **This is important for applications were a reduction in capacity could cause availability issues for users.**

**In case of failure**
- You need to perform an additional rolling update to roll back the changes

#### Immutable

![Immutable](./images/eb_immutable.png)

1. Create a new ASG group with EC2 instance
2. Deploy the updated version of the app on the new EC2 instances
3. Point the ELB to the new ASG and delete the old ASG which will terminate the old EC2

#### EB - Deployment Methods


| Method        | Impact of failed deployment | Deploy time | No downtime | No DNS change | Rollback process | Code deployed to instances
| ------------- |:-------------:| :-----:|:-----:| :-----:|:-----:| :-----:|
| All at once   | Downtime | O    | False | True | Manual | Existing | 
| Rolling | Single batch out of service | OO*  | True | True | Manual | Existing |
| Rolling with additional batch |Minimal if first batch fails | OOO* | True | True | Manual | New and Existing |
| Immutable | Minimal | OOOO | True | True | Terminate New | New |
| Blue/Green | Minimal | OOOO | True | False | Swap URL | New |

* times may vary

#### In-Place vs Blue/Green Deployment

*In-Place and Blue/Green Deployment **are not definitive in definition** and the context can change the scope of what they mean*

- In-Place could mean within the scope of Elastic Beanstalk Env
All the deployment policies provided by EB could be considered In-Place since they are within the scope of a single EB environment
  - All at once
  - Rolling
  - Rolling with additional
  - Immutable
- In-Place could mean within the scope of the same server (not replacing the server)
Deployment policies with do not involve the server being replaced
  - All at once
  - Rolling
In-Place could mean within the scope of an uninterupted server
Traffic is never routed away from the server (taken-of-service). Implements Zer-downtime deploys where Blue/Greens accurs on the server
  - EB can't do this
  - Ruby on Rails + Unicorn is an example of this method
  
Blue/Green deployment in the context of Elastic Beanstalk

![In-Place vs Blue/Grean](./images/eb_in-place_vs_blue-green.png)

#### Configuration Files

- Elastic Beanstalk environments can be customized used configuration files
 - **.ebextensions** is a hidden folder called at the root of your project which contains the config files
 - **.config** is the extension for the config files which need to be stored in ebextensions
 
- Configuration files can config
  1. Option Settings
  2. Linux/Windows Server Configuration
  3. Custom Resources
  
#### Env Manifest

- The Environment manifest is a file called **env.yml** which is stored at the root of your project
When creating new Elastic Beanstalk environments this file allows you to configure the defaults such as:

![Env Manifest](./images/eb_env_manifest.png)

#### Linux Server Configuration

- Packages
  - download and install prepackaged applications and components
- Groups
  - create Linux/UNIX groups and to assign group IDs
- Users
  - create Linux/UNIX users
- Files
  - create files on the EC2 instance (inline or from URL)
- Commands
  - execute commands on the EC2 instance before app is setup
- Services
  - define which services should be started or stopped when the instance is launched
- Container Commands
  - execute commands that affect your application source code

#### EB CLI

The CLI is hosted on Github
You run these two commands to install

- Commands
  - **eb init** - configure your project directory and the EB CLI
  - **eb create** - create your first env
  - **eb create** - see the current status of your env
  - **eb** view health info about the instances and the state of your overall env (use --refresh to upddate every 10 seconds)
  - **eb events** - see a list of events output by EB
  - **eb logs** - pull logs from an instance in your env
  - **eb open** - open your env's website in a browser
  - **eb deploy** - once the env is running, deploy and update
  - **eb config** - take a look at the configuration optiuons available for your running env
  - **eb terminate** - delete the environment
  
  #### EB Custom Image
  
- When you create an EB environment, you can specify an dAMI to use instead of the standard EB AMI
- A custom AMI can improve provisioning times when instances are launched in your environment
- If you need to install a lot of software that isn't included in the standard AMIs

![Custom Image](./images/eb_custom_image.png)

#### Configuration RDS

- A database can be added inside or outside your EB environment

![Configuring RDS](./images/eb_configure_rds.png)

#### Elastic Beanstalk Cheat Sheet

- **Elastic Beanstalk** handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring
- When you want to run a web-application but you don't wahnt to have to think about the underlying infrastructure
- It costs nothing to use Elastic Beanstalk (only the resources it provisions eg. RDS. ELB, EC2)
- Recommended for test or development apps. Not recommended for production use
- You can choose from the following preconfigured platforms: Java, .NET, PHP, Node.js, Python, Ruby, Go and Docker
- You can run containers on EB either in Single-container or Multi-container, these containers are running on ECS instead of EC2
- You can launch either a **Web Environment** or a **Worker Environment** 
  - **Web Environments** come in two types **Single-Instance** or **Load Balanced**
    - **Single-Instance Env** launches a single EC2 instance, an EIP is assigned to the EC2
    - **Load Balanced Env** launch EC2s behind an ELB managed by an ASG
  - **Worker Environments** creates an SQS queue, install the SQS daemon on the EC2 instances, and has ASG scaling policy which will add or remove instances based on queue size
- EB has the following **Deployment Policies**
  - **All at once** takes all servers out-of-service, applies changes, puts servers back-in-service, Fast, has downtime
  - **Rolling** updates servers in batches, reduced capacity based on batch size
  - **Rolling with additional batches** adds new servers in batches to replace old, never reduces capacity
  - **Immutable** creates the same amaount of servers, and switches all at once to new servers, removing old servers
- Rolling deployment policies require an **ELD** so cannot be used with Single-Instance Web Environments
- In-Place deployment is when deployment occurs whitin the environment, all deployment policies are In-Place
- Blue/Green is when deployment swaps environments (outside an environment), when you have external resources such as RDS which cannot be destroyed its suited for Blue/Green
- **bextensions**s a folder which contains all configuration files
- With EB you can provide **Custom Images** which can improve provisioning times
- If you let Elastic Beanstalk create the RDS instance, that means when you delete your environment it will delete the database. This setup is inteded for development and test environments
- **Dockerrun.aws.json** is similar to an ECS Task Definition files and defines multi-container configuration


### Elastic Beanstalk Follow Along

#### Cloud9 Setup

- Make sure you are in the right region!
- Create a developer environment in Cloud9 through the AWS console

#### Security Groups

Once you have your web application we will need to open up the ports
- By default Cloud9 have ports 8080, 8081, 8082 open
1. Identify the MAC Address with `curl -s http://169.254.169.254/latest/meta-data/mac`
2. Find the security group using `curl -s http://169.254.169.254/latest/meta-data/network/interfaces/macs/**yourMacId**/security-group-ids`
3. Find your IP address by going to http://checkip.amazonaws.com/
4. We will need the IP address to add to the cidr block
5. Use the command `aws ec2 authorize-security-group-ingress --group-id **yourSecurityGroupID** --port 8080 --protocol tcp --cid **yourIP**/32`
*the /32 at the end. 
5. Use the command `aws ec2 authorize-security-group-ingress --group-id **yourSecurityGroupID** --port 8080 --protocol tcp --cidr **yourIP**/32`
*The /32 at the end of the cidr block is important because it says only this IP address*
6. Check that your Security Group has been edited `aws ec2 describe-security-groups --group-ids **yourSecurityGroupID**  --output text --filters Name=ip-permission.to-port,Values=8080`
7. If the Security Group is not set nothing would show otherwise it should look something like this:
```
SECURITYGROUPS  Security group for AWS Cloud9 environment aws-cloud9-DevEnv-08e6543c08554c57a272f337df0f96df sg-0938552a4807d9570    aws-cloud9-DevEnv-08e6543c08554c57a272f337df0f96df-InstanceSecurityGroup-2AM4ALIQ5DHX        540908314583    vpc-fdd1c687
IPPERMISSIONS   8080    tcp     8080
IPRANGES        76.126.6.216/32
IPPERMISSIONS   22      tcp     22
IPRANGES        35.172.155.192/27
IPRANGES        35.172.155.96/27
IPPERMISSIONSEGRESS     -1
IPRANGES        0.0.0.0/0
TAGS    aws:cloud9:owner        AIDAX34FF37LSKQTQVJES
TAGS    aws:cloudformation:stack-id     arn:aws:cloudformation:us-east-1:540908314583:stack/aws-cloud9-DevEnv-08e6543c08554c57a272f337df0f96df/1a523520-ac14-11ea-b406-0e706f74ed45
TAGS    aws:cloudformation:logical-id   InstanceSecurityGroup
TAGS    Name    aws-cloud9-DevEnv-08e6543c08554c57a272f337df0f96df
TAGS    aws:cloudformation:stack-name   aws-cloud9-DevEnv-08e6543c08554c57a272f337df0f96df
TAGS    aws:cloud9:environment  08e6543c08554c57a272f337df0f96df
```
8. Next find the public ip with the command `curl -s http://169.254.169.254/latest/meta-data/public-ipv4`
9. Run your web application and check to see if it runs at the IP and port 8080 (eg. 54.165.37.183:8080)
10. Add your project to a Git repo

#### EB CLI Setup

1. We will download the EB CLI following the directions here: https://github.com/aws/aws-elastic-beanstalk-cli-setup
2. Make sure to add the eb cli to PATH given their recommended command `echo 'export PATH="/home/ec2-user/.ebcli-virtual-env/executables:$PATH"' >> ~/.bash_profile && source ~/.bash_profile` and `echo 'export PATH=/home/ec2-user/.pyenv/versions/3.7.2/bin:$PATH' >> /home/ec2-user/.bash_profile && source /home/ec2-user/.bash_profile` if you are using bash

#### EB init

