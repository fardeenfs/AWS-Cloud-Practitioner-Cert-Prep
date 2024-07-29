# AWS Cloud Practitioner Preparation

### IAM

- **Users:** mapped to a physical user, has a password for AWS Console
- **Groups:** contains users only
- **Policies:** JSON document that outlines permissions for users or groups
- **Roles:** for EC2 instances or AWS services
- **Security:** MFA + Password Policy
- **AWS CLI:** manage your AWS services using the command-line
- **AWS SDK:** manage your AWS services using a programming language
- **Access Keys:** access AWS using the CLI or SDK
- **Audit:** Credential Reports & IAM Access Advisor

### EC2

- **EC2 Instance:** AMI (OS) + Instance Size (CPU + RAM) + Storage + Security Groups + EC2 User Data
- **Security Groups:** Firewall attached to the EC2 instance
- **EC2 User Data:** Script launched at the first start of an instance
- **SSH:** start a terminal into our EC2 Instances (port 22)
- **EC2 Instance Role:** link to IAM roles
- Purchasing Options:
    - **On-Demand**
        - Pay for what you use.
        - Linux or Windows - billing per second after the first minute. Billing per hour for all other operating systems
        - Has the highest cost but no upfront payment
        - No long term commitment.
        - Recommended for **short term** and **un-interrupted workloads**, where you can’t predict how the application will behave.
    - **Reserved Instances**
        - Upto 72% discount compared to On-demand. (Can change)
        - You reserve a specific instance attribute (Instance Type, Region, Tenancy, OS)
        - **Reservation Period** - 1 year (+discount) or 3 years (+++discount)
        - **Payment Options** - No Upfront (+), Partial Upfront (++), All Upfront (+++)
        - **Reserved Instance’s Scope** - Regional or Zonal (reserve capacity in an AZ)
        - Recommended for steady-state usage applications (think database)
        - You can buy and sell in the Reserved Instance Marketplace
        - **Convertible Reserved Instance:** Allows you to change the EC2 instance type, instance family, OS, scope and tenancy. Upto 66% discount
    - **Savings Plans**
        - Get a discount based on long-term usage (upto 72% - same as RIs)
        - Commit to a certain type of usage ($10/hour for 1 or 3 years)
        - Usage beyond EC2 Savings Plans is billed at the On-Demand price
        - Locked to a specific instance family and AWS region
        - Can change instance size, OS and tenancy (Host, Dedicated, Default)
    - **Spot Instances**
        - Can get a discount of up to 90% compared to On-demand
        - Instances that you can “lose” at any point of time is your max price is less than the current spot price
        - The **MOST cost-efficient** instances in AWS
        - Useful for workloads that are resilient to failure - Batch jobs, Data analysis, Image processing, Any distributed workloads, Workloads with a flexible start and end time
        - Not suitable for critical jobs or databases
    - **Dedicated Hosts**
        - A physical server with EC2 instance capacity fully dedicated to your use
        - Allows you address compliance requirements and use your existing server-bound software licenses (per-socket, per-core, per-VM software licenses)
        - Purchasing Options:
            - On-demand: Pay per second for active. Dedicated Host.
            - Reserved: 1 or 3 years (No Upfront, Partial Upfront, All Upfront)
        - Most **Expensive** Option
        - Useful for software that have complicated licensing model (BYOL - Bring Your Own License) or for companies that have strong regulatory or compliance needs.
    - **Dedicated Instances**
        - Instances run on hardware that’s dedicated to you.
        - May share hardware with other instances in the same account.
        - No control over instance placement (can move hardware after Stop/Start)
    - **Capacity Reservations**
        - Reserve On-Demand instances capacity in a specific AZ for any duration
        - You always have access to EC2 capacity when you need it
        - No time commitment (create/cancel anytime), no billing discounts
        - Combine with Regional Reserved Instances and Savings Plans to benefit from billing discounts
        - Charged at On-Demand rate whether you run instances or not
        - Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ
    

### EC2 Instance Storage

- **EBS volumes**
    - Network drives attached to one EC2 instance at a time
    - Mapped to an AZ
    - Can use EBS Snapshots for backup/transfer our EBS volumes across AZ
- **AMI**: Create ready-to-use EC2 instances with our customizations
- **EC2 Image Builder**: Automatically build, test and distribute AMIs
- **EC2 Instance Store**
    - High performance hardware disk attached to our EC2 instance
    - Lost if our instance is stopped/terminated
- **EFS:** Network file system, can be attached to 100s of instances in a region
- **EFS-IA:** Cost-optimized storage class for infrequent accessed file
- **FSx**
    - Fully managed service to launch 3rd party high performance file systems on AWS. Alternative for EFS.
    - **FSx for Windows:** Network file system for Windows servers
    - **FSx for Lustre:** High Performance Computing Linux file system
    

### Elastic Load Balancing (ELB) and Auto Scaling Groups (ASG)

- **High Availability** vs **Scalability** (vertical and horizontal) vs **Elasticity** vs **Agility** in the Cloud
- **Elastic Load Balancers (ELB)**
    - Distribute traffic across backend EC2 instances, can be Multi-AZ
    - Supports health checks
    - 4 types: Classic(old), Application (HTTP - L7), Network (TCP - L4), Gateway (L3)
    - **Application Load Balancer**
        - HTTP/HTTPS/gRPC protocols (Layer 7)
        - HTTP Routing features
        - Static DNS (URL)
    - **Network Load Balancer**
        - TCP/UDP protocols (Layer 4)
        - High Performance: millions of request per seconds
        - Static IP through Elastic IP
    - **Gateway Load Balancer**
        - GENEVE Protocol on IP Packets (Layer 3)
        - Route Traffic to Firewalls that you manage on EC2 Instances
        - Intrusion detection
- **Auto Scaling Groups (ASG)**
    - Implement Elasticity for your application, across multiple AZ
    - Scale EC2 instances based on the demand on your system, replace unhealthy
    - Integrated with ELB

### Amazon S3

- Buckets vs Objects: Global unique name, tied to a region
- **S3 Security:** IAM policy, S3 Bucket Policy (public access), S3 Encryption
- **S3 Websites:** Host a static website on Amazon S3
- **S3 Versioning:** Multiple versions for files, prevent accidental deletes
- **S3 Replication:** Same-Region or Cross-Region, must enable versioning
- **S3 Storage Classes:** Standard IA, IZ-IA, Intelligent, Glacier (Instance, Flexible, Deep)
- **Snow Family:** Import data onto S3 through a physical device, edge computing
    - **Snowcone:** 8TB HDD or 14 TB SSD | Upto 24 TB | [Online and offline]
    - **Snowball Edge:** 80TB - 210 TB | Upto Petabytes of data | [Offline only]
    - **Snowmobile:** <100PB | Upto Exabytes of data | [Offline only]
- **OpsHub:** Desktop application to manage Snow Family devices
- **Storage Gateway:** Hybrid solution to extend on-premises storage to S3

### Database and Analytics

- **RDS:** Managed AWS service for SQL. Can’t SSH into instance (vs DB on EC2)
- **Aurora:** Proprietary AWS service which is faster and supports PostgreSQL and MySQL
- **Aurora Serverless:** Automated database instantiation and autoscaling based on actual usage.
- **ElastiCache:** In-memory cache for all databases. Managed **Redis** or **Memcached**
- **DynamoDB:** Manage AWS service for NoSQL
- **DAX:** Cache for DynamoDB
- **DocumentDB:** “Aurora for MongoDB”. Proprietary AWS service which is faster for MongoDB
- **Redshift:** Warehouse OLAP. Based on PostgreSQL. (SQL)
- **EMR (Elastic Map Reduce):** Used for big data with clustering (Hadoop clusters)
- **Athena:** Query data on Amazon S3
- **QuickSight:** Dashboard on your data (serverless)
- **Neptune:** Managed graph database. Used for datasets like for a social network. High availability with replications across multiple AZs
- **Timestream:** Time series database.
- **Amazon QLDB:** Financial Transactions Ledger (immutable journal, cryptographically verified). Central database
- **Amazon Managed Blockchain:** Managed Hyperledger Fabric & Ethereum blockchains. Decentralized database
- **Glue:** Managed ETL (Extract Transform Load) and Data Catalog service
- **Database Migration Service:** Move data between databases.

### Other Compute

- **Docker:** Container technology to run applications
- **ECS:** Run docker containers on EC2 instances
- **Fargate**
    - Run Docker containers without provisioning the infrastructure
    - Serverless offering (no EC2 instances)
- **ECR:** Private Docker Images Repository
- **Batch:** Run batch jobs on AWS across managed EC2 instances
- **Lightsail:** Predictable and low pricing for simple application and DB stacks
- **Lambda**
    - Lambda is Serverless, Function as a Service, seamless scale, reactive
    - Lambda Billing
        - By the time run * by the RAM provisioned
        - By the number of invocations
    - Language Support: many programming languages except (arbitary) Docker
    - Invocation time: up to 15 minutes
- **API Gateway:** Expose Lambda functions as HTTP API

### Deployment

- **CloudFormation** (AWS only)
    - Infrastructure as Code, works with almost all of AWS resources
    - Repeat across Regions & Accounts
- **Beanstalk** (AWS only)
    - Platform as a Service (PaaS), limited to certain programming languages or Docker
    - Deploy code consistently with a known architecture. Example: ALB + EC2 + RDS
- **CodeDeploy** (hybrid)
    - Deploy and upgrade any application onto servers
- **Systems Manager** (hybrid)
    - Patch, configure and run commands at scale

### Developer Services

- **CodeCommit:** Store code in private git repository (version controlled)
- **CodeBuild:** Build & test code in AWS
- **CodeDeploy:** Deploy code onto servers
- **CodePipeline:** Orchestration of pipeline (from code to build to deploy)
- **CodeArtifact:** Store software packages/dependencies on AWS
- **CodeStar:** Unified view for allowing developers to do CI/CD and code
- **Cloud9:** Cloud IDE with collaborative features
- **AWS CDK:** Define your cloud infrastructure using a programming language for a CloudFormation template.

### AWS Global Infrastructure

- **Route 53** (Global DNS)
    - Great to route users to the closest deployment with least latency
    - Great for disaster recovery strategies
- **CloudFront** (Global Content Delivery Network)
    - Replicate part of application to AWS Edge Locations - decreased latency
    - Cache common requests - improved user experience and decreased latency
- **S3 Transfer Acceleration**
    - Accelerate global uploads and downloads into Amazon S3.
- **AWS Global Accelerator**
    - Improve global application availability and performance using the AWS global network
- **AWS Outposts**
    - Deploy outposts racks in your own Data Centers to extend AWS services
- **AWS Wavelength**
    - Brings AWS services to the edge of the 5G networks
    - Ultra-low latency application
- **AWS Local Zones**
    - Bring AWS resources (compute, database, storage) closer to your users
    - Good for latency-sensitive applications

### Cloud Integrations

- **SQS**
    - Queue service in AWS
    - Multiple Producers, messages are kept upto 14 days
    - Multiple Consumers, share the read and delete messages when done
    - Used to **decouple** applications in AWS
- **SNS**
    - Notification service in AWS
    - Subscribers: Email, Lambda, SQS, HTTP, Mobile
    - Multiple Subscribers, send all messages to all of them
    - No message retention
- **Kinesis:** Real-time data streaming, persistence and analysis
- **Amazon MQ:** managed message broker for ActiveMQ and RabbitMQ in the cloud (MQTT, AMQP protocols)

### Cloud Monitoring

- **CloudWatch**
    - **Metrics:** Monitor the performance of AWS services and billing metrics
    - **Alarms:** Automate notification, perform EC2 action, notify to SNS based on metric
    - **Logs:** collect log files from EC2 instances, servers, Lambda functions…
    - **Events (or EventBridge):** React to events in AWS, or trigger a rule on a schedule.
- **CloudTrail:** Audit API calls made within your AWS account
- **CloudTrail Insights:** Automated analysis of your CloudTrail Events
- **X-Ray:** Trace requests made through your distributed applications
- **AWS Health Dashboard:** status of all AWS services across all regions
- **AWS Account Health Dashboard:** AWS events that impact your infrastructure
- **Amazon CodeGuru:** Automated code reviews and application performance recommendation.

### Virtual Private Cloud (VPC) and Networking

- **Subnets:** Tied to an AZ, network partition of the VPC
- **Internet Gateway:** At the VPC level, provide Internet Access
- **NAT Gateway/Instances:** Give internet access to private subnets
- **NACL:** Stateless, subnet rules for inbound and outbound
- **Security Groups:** Stateful, operate at the EC2 instance level or ENI
- **VPC Peering:** Connect two VPC with non overlapping IP ranges, nontransitive
- **Elastic IP:** Fixed public IPv4, ongoing cost if not in-use
- **VPC Endpoints:** Provide private access to AWS services within VPC
- **PrivateLink:** Privately connect to a service in a 3rd party VPC
- **VPC Flow Logs:** Network traffic logs
- **Site to Site VPN:** VPN over public internet between on-premises DC and AWS
- **Client VPN:** OpenVPN connection from you computer into you VPC
- **Direct Connect:** Direct Private connection to AWS
- **Transit Gateway:** Connect thousands of VPC and on-premises networks together.

### Security and Compliance

- **Shield:** Automatic DDoS Protection + 24/7 support for advanced
- **WAF:** Firewall to filter incoming requests based on rules
- **KMS:** Encryption keys managed by AWS
- **CloudHSM:** Hardware encryption, we manage encryption keys
- **AWS Certificate** Manager: Provision, manage, and deploy SSL/TLS Certificates
- **Artifact:** Get access to compliance reports such as PCI, ISO, etc…
- **GuardDuty:** Find malicious behaviour with VPC, DNS & CloudTrail Logs
- **Inspector:** Find software vulnerabilities in EC2, ECR Images, and Lambda functions
- **Network Firewall:** Protect VPC against network attacks
- **Config:** Track config changes and compliance against rules
- **Macie:** Find sensitive data (ex: PII) in Amazon S3 buckets
- **CloudTrail:** Track API calls made by users within account
- **AWS Security Hub:** Gather security findings from multiple AWS accounts
- **Amazon Detective:** Find the root cause of security issues or suspicious activities
- **AWS Abuse:** Report AWS resources used for abusive or illegal purposes
- **Root User Privileges:**
    - Change account settings
    - Close your AWS account
    - Change or cancel your AWS Support plan
    - Register as a seller in the Reserved Instance Marketplace
- **IAM Access Analyzer: Identify which resources are shared externally**
- **Firewall Manager:** Manage security rules across an Organization (WAF, Shield)

### Machine Learning

- **Rekognition:** Face detection, labeling, celebrity recognition
- **Transcribe:** Audio to text (ex: subtitles)
- **Polly:** Text to audio
- **Translate:** Translations
- **Lex:** Build conversational bots - chatbots
- **Connect:** Cloud contact center
- **Comprehend:** Natural language processing of text
- **SageMaker:** Machine learning for every developer and data scientist
- **Forecast:** Build highly accurate forecasts
- **Kendra:** ML-powered search engine
- **Personalize:** Real-time personalized recommendations

### Billing and Costing Tools

- **Compute Optimizer:** Recommends resources’ configurations to reduce cost
- **Pricing Calculator:** Cost of services on AWS
- **Billing Dashboard:** High level overview + free tier dashboard
- **Cost Allocation Tags:** Tag resources to create detailed reports
- **Cost and Usage Reports:** Most comprehensive billing dataset
- **Cost Explorer:** View current usage (detailed) and forecast usage
- **Billing Alarms:** In us-east-1. Track overall and per-service billing
- **Budgets:** More advanced. Track usage, costs, RI, and get alerts
- **Savings Plans:** Easy way to save based on long-term usage of AWS

### Account Best Practices

- Operate multiple accounts using **Organizations**
- Use **SCP** (Service control policies) to restrict account power
- Easily setup multiple accounts with best-practices with **AWS Control Tower**
- Use **Tags & Cost Allocation Tags** for easy management & billing
- **IAM guidelines**: MFA, least-privilege, password policy, password rotation
- **Config** to record all resources configurations & compliance over time.
- **CloudFormation** to deploy stacks across accounts and regions
- **Trusted Advisor** to get insights, Support Plan adapted to your needs
- Send Service Logs and Access to **S3** or **CloudWatch Logs**
- **CloudTrail** to record API calls made within your account
- **If your Account is compromised:** change the root password, delete and rotate all passwords/keys, contact the AWS support
- Allow user to create pre-defined stacks defined by admins using **AWS Service Catalog**

### Advanced Identity

- **IAM**
    - Identity and Access Management inside your AWS account
    - For users that you trust and belong to your company
- **Organizations:** Manage multiple accounts
- **Security Token Service (STS):** temporary, limited-privileges credentials to access AWS resources
- **Cognito:** create a database of users for your mobile & web applications
- **Directory Services:** integrate Microsoft Active Directory in AWS
- **IAM Identity Center:** one login for multiple AWS accounts & applications

### Other Services

- **Amazon Workspaces:** Managed Desktop as A Service solution to provision Windows or Linux desktops. Great to eliminate management of on-premise VDI.
- **AppStream 2.0:** Application streaming service which is delivered within a web browser.
- **IoT Core:** Allows connection of IoT devices to the AWS Cloud
- **AppSync:** Store and sync data across mobile and web apps in real-time. Makes use of GraphQL
- **Amplify:** A set of tools and services that helps you develop and deploy scalable full stack web and mobile applications
- **Application Composer:** Visually design and build serverless applications quickly on AWS
- **Device Farm:** Fully-managed service that tests your web and mobile apps against desktop browsers, real mobile devices, and tablets
- **AWS Backup:** Fully-managed service to centrally manage and automate backups across AWS services
- **AWS Elastic Disaster Recovery (DRS):** Quickly and easily recover your physical, virtual, and cloud based servers into AWS
- **DataSync:** Move large amount of data from on-premises to AWS
- **Cloud Migration Strategies (The 7Rs)**
    - **Retire:** Turn of things that you don’t need
    - **Retain:** Do nothing for now (it’s still a decision to make). No business value to migrate, mainframe or mid-range and non-x86 Unix apps
    - **Relocate:** Move apps from on-premises to its Cloud version
    - **Rehost** **(“lift and shift”):** Simple migrations by re-hosting on AWS (applications, databases, data…). Migrate machines. No cloud optimizations, migrate as is.
    - **Replatform (”lift and reshape”):** Not changing core architecture, but leverage some Cloud optimizations
    - **Repurchase (“drop and shop”):** Moving to a different product while moving to the cloud
    - **Refactor/Re-architect:** Reimagining how the application is architected using Cloud Native features.
- **Application Discovery Service:** Plan migration projects by gathering information about on-premises data centers
- **Migration Evaluator:** Helps you build a data-driven business case for migration to AWS
- **Migration Hub:** Central location to collect servers and application inventory data for the assessment, planning, and tracking of migration to AWS
- **AWS Fault Injection Simulator (FIS):** Fully managed service for running fault injection experiments on AWS workloads. Based on **Chaos engineering**
- **AWS Step Functions:** Build serverless visual workflow to orchestrate your lambda functions
- **AWS Ground Station:** Fully managed service that lets you control satellite communications, process data, and scale your satellite operations
- **AWS Pinpoint:** Scalable 2-way (outbound/inbound) marketing communications service. Ability to segment and personalize messages with the right content to customers

### AWS Architecting & Ecosystem

- Well Architected Framework (6 Pillars)
    1. **Operational Excellence:** Includes the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures
    2. **Security:** Includes the ability to protect information, systems, and assets while delivering business value through risk assessment and mitigation strategies
    3. **Reliability:** Ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues
    4. **Performance Efficiency:** Includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve
    5. **Cost Optimization:** Includes the ability to run systems to deliver business value at the lowest price point
    6. **Sustainability:** The sustainability pillar focuses on minimizing the environmental impacts of running cloud workloads
- Cloud Adoption Framework
    - **Business Perspective** helps ensure that your cloud investments accelerate your digital transformation ambitions and business outcomes.
    - **People Perspective** serves as a bridge between technology and business.
    - **Governance Perspective** helps you orchestrate your cloud initiatives while maximizing organizational benefits and  minimizing transformation-related risks.
    - **Platform Perspective** helps you build an enterprise -grade, scalable hybrid cloud platform.
    - **Security Perspective** helps you achieve the confidentiality, integrity, and availability of your data and cloud workloads.
    - **Operations Perspective** helps ensure that your cloud services are delivered at a level that meets the needs of your business.