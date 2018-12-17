[AWS](aws.md)

# Google Cloud Platform

## Physical

* vCPU
* Physical server
* Rack
* DataCentre (building)
* Zone
* Region
* Multi-Region (US, Asia, Europe)
* Private Global Network (don'e go to Internet)
* Points of Presence (PoP). Network edges and CDN locations
* Global system

### Network difference

A normal network routes the traffic to the edge location closest to destination.
Google network routes the traffic to the edge location closest to the source, this allows using a single global IP that can load balance worldwide.

### Pricing
* Provisioned: to be ready to handle X load
* Usage: handle whatever I use
* Network traffic
    * Free ingress (incoming)
    * Charged egress (outgoing)

### Security
* Separation of duties and physical security
* Absolutely everything encrypted at rest
* String key and identity management
* Network encryption:
    * All control information (Google Console) encrypted
    * WAN traffic to be encrypted automatically
    * Moving towards encrypting all traffic within DCs
* Distrust the network, anyway. See [BeyondCorp](https://cloud.google.com/beyondcorp/)

### Scale & automation
* No limits
* Can configure resource quotas per:
    * scope:
        * Regional
        * Global
    * Changes:
        * Automate
        * By request
    * Can be queryed

### Organization
A project is similar to an AWS Account (ADD LINK!!). 
It contains resources and can be grouped and controlled in a hierarchy.


## Services

### Compute

#### Compute Engine
Similar to [EC2](https://aws.amazon.com/ec2/)
* VM on demand
* Custom CPU and RAM
* Pay by seconds

#### Kubernetes Engine
Similar to [ECS](https://aws.amazon.com/ecs/) & [EKS](https://aws.amazon.com/eks/)
* Managed Kubernetes cluster with autoscaling
* Kubernetes DNS on by default for service discovery
* No IAM (ADD LINK!!)
* Integration with Persistent Disk (ADD LINK!!)

#### App Engine
Similar to [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
* PaaS that takes code and runs it
* Autoscale (up and down) based on load
* Pay per underlying GCE instances

#### Cloud Functions
Similar to [Lambda](https://aws.amazon.com/lambda)
* NodeJS code to respond to an event
* Also known as FaaS or Serverless
* Pay per CPU and RAM assigned per 100ms
* Gets an HTTP endpoint automatically


### Persistance

#### Local SSD
Similar to EC2 Instance Store Volumes
* SSD physically attached to server
* DATA WILL BE LOST WHENEVER THE INSTANCE IS SHUT DOWN!!

#### Persistent Disk
Similar to [Elastic Block Storage](https://aws.amazon.com/ebs/)
* Network attached
* Boot disk for GCE instances
* Performace scales with volume size, but slower than SSD
* Replicated for durability
* Can be resized, but still needs filesystem update in VM
* Save image snapshots

#### Cloud SQL
Similar to [Amazon RDS](https://aws.amazon.com/rds/)
* Managed and reliable MySQL and PostgreSQL
* Automatic replication, backup, failover, ...
* Scaling is manual
* Pay per underlying GCE and persistent disk, pluss fees

#### Cloud Spanner
* Horizoltally scalable, strongly consistent, relational service
* From one to thousands of nodes. Recomemded at least 3 for production
* SLA 99.999%
* Pay per node, time and storage

#### Big Query
Similar to [Amazon Athenea](https://aws.amazon.com/athena/)
* Serverless column-store for analytics uaing SQL
* Pay per usage time and storage, no per GCE
* Scales internally, scan TBs in seconds and PB in minutes
* Caches for 24 hours for free

#### Cloud Datastore
Similar to [DynamoDB](https://aws.amazon.com/dynamodb/) or MongoDB
* Managed, autoscaled NoSQL with indexes, queries, ACID
* "Built-in" indexes for filtering and manual "composite" indexes for complex, they can "explode" be aware
* Pay per storage and IO operations

#### Firebase Database & Cloud Firestore
* NoSQL with realtime client update via websocket
* Single JSON doc, only in US
* Collections contain documents that contain data

#### Cloud Storage
Similar to [S3](https://aws.amazon.com/s3/)
* Scalable, managed, versioned, highly durable object storage in buckets
* Integrated site hosting and CDN
* Lifecycle transitions across classes, that differ in cost and availability but same latency:
    * Multi-region
    * Region
    * Newline
    * Coldline
* Pay peroperation and GB stored

#### Data Transfer Appliance
Similar to [AWS Snowball](https://aws.amazon.com/snow/)
* To physically ship data to GCS
* 100 - 480 TB

#### Storage Transfer Service
* Copies from source to GCS bucket
* Sources:
    * S3
    * HTTP endpoint
    * Another bucket
* One time or scheduled


### Networking

#### Google Domains
Similar to [Amazon Route 53](https://aws.amazon.com/route53/)
* Built-in DNS
* Supports DNSSEC
* Email forwarding with automatic setup of SPF and DKIM

#### Cloud DNS
Similar to [Amazon Route 53](https://aws.amazon.com/route53/)
* Scalable, reliable, managed, authoritative DNS
* 100% uptime
* Low latency globally
* Supports DNSSEC
* Managed via UI, CLI and API
* Pay per hosting zone and DNS lookup

#### Static IP
Similar to Elastic IP Address
* Reserve IPs in projects and assing them to resources
* Types:
    * Regional IP: for GCE instances & network LB
    * Global IP: for global LB, HTTPS, SSL proxy, TCP proxy, ...
* Pay per reserved IP not in use

#### Load balancing
Similar to [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/)
* High performance, scalable with autoscaling and Cloud DNS
* Naturally handles spikes without prewarming
* Regional LB: healthchecks, round robin, session affinity
* Global LB: multi-region failover for HTTP
    * Prioritize low-latency connection to region near to user, than gentle fail over
* As it's built into Google Network, it can react quickly to changes in users, network, ...

#### Cloud CDN
Similar to [CloudFront](https://aws.amazon.com/cloudfront/)
* Integrated with GCE and GCS
* Supports HTTP 2 but no custom origins, only to get data from GCP
* Configuring this is just a checkbox on the load balancer
* Pay per request volume and invalidation requests

#### VCP (Virtual Private Cloud)
Similar to [Amazon VPC](https://aws.amazon.com/vpc/)
* Global IPv4 unicat SDN (Software Defined Network) for GCP resources
* Modes:
    * Automatic: easy
    * Custom: gives control
* Configure subnets, routes, Firewalls, VPN, BGP
* VPC is global
* Subnet are regional
* VPC can be shared across many projects in same organization
* Can enable provate access to some GCP services
* Free to configure

#### Cloud Interconnect
* Options for connecting external networks to Google's network
* Private connection to VPC via CloudVPN or Dedicated Interconnect (with SLAs)
* Public Google Services accesible via External Peering (No SLAs)
* Reduces egress fees

#### Cloud VPN
Similar to AWS VPN
* IP Sec VPN to connect to VPC via public internet for low volume connection
* For persistent, static connections between gateways, no dynamic clients. Per VON gateway must have a static IP
* Encrypted link to VPC (as opposed to Dedicated Interconnect), into one subnet
* Support bot static and dynamic routing

#### Dedicated Interconnect
Similar to [AWS DirectConnect](https://aws.amazon.com/directconnect/)
* Physical link between VPC and on-prem for high volume
* VLAN attachment is private connection to VPC in one region, no public GCP APIs
* No encrypted
* Can setup redundant connections for critical apps

#### Cloud Router
* Dynamic routing based on BGP (Boarder Gateway Protocal ADD LINK!!) for hybrid  between GCP VPCs and external networks
* Works with CloudVPN and Dedicated Interconnect
* Automatically learns subnets in VPC and anounces them to on-prem
* Without router you need to manage static routes for VPN

#### CDN Interconnect
* Direct, low-latency connectivity to some CDN providers


### Machine Learning

#### Cloud ML Engine
Similar to [Amazon Machine Learning](https://aws.amazon.com/sagemaker/)
* Managed service for training ML models & making predictions
* Integrated with GCS and BQ, Cloud Datalab, Cloud Dataflow
* Supports online and batch processing, or download and make predictions on devices
* HyperTune automatically tunes model hyperparameters to avoid manual tuning
* Pay per hour

#### Cloud Vision API
Similar to [Amazon Rekognition](https://aws.amazon.com/rekognition/)
* Clasifies images, detect object/faces, find/read text, ...
* Pre-trained ML model

#### Cloud Speech API
* Spoken words to text
* +110 languages and variations
* Pre-recorded or real-time audio

#### Cloud Natural Language API
* Analyzes text for sentiment, intent, content classification and extracts information

#### Cloud Translation API

#### DialogFlow
Similar to [Amazon Lex](https://aws.amazon.com/lex/)
* ChatBot
* Free
* Train it, or pre-built

#### Cloud Video Intelligence API
* Annotates videos in GCS with information about what they contain
* Adult content warning

#### Cloud Job Discovery Service
* Helps career sites
* Integrated with many job/hiring systems


### Big Data

#### Cloud IoT Core
Similar to [AWS IoT](https://aws.amazon.com/iot-core/)
* Managed service to connect, manage and ingest from devices globally
* Device manager handle device identity, authentication, configuration and control
* Protocol bridge publishes incoming telemetry to Cloud Pub/Sub

#### Cloud Pub/Sub
Similar to [Amazon SNS](https://aws.amazon.com/sns/), [Amazon SQS](https://aws.amazon.com/sqs/), Amazon Kinesis, Kafka
* Scalable at-least-once messaging for ingestion
* Global by default
* Messages up to 10MB stored for 7 days

#### Cloud Data Prep
Similar to [AWS Glue](https://aws.amazon.com/glue/)
* Visually explore, clean and prepare data for analysis with no servers

#### Cloud Data Proc
Similar to [Amazon EMR](https://aws.amazon.com/emr/)
* Betch MapReduce via managed Spark & Hadoop clusters

#### Cloud DataFlow
* smartly-autoscaled-managed betch or stream MapReduce-like processing

#### Cloud Datalab
* Interactive tool for data exploration, analysis, visualization and ML
* Uses Jupiter Notebook

#### Cloud DataStudio
Similar to [Amazon QuickSight](https://aws.amazon.com/quicksight/)
* BigData visualization

#### Cloud Genomics


## Security & identity

### Roles
Similar to [AWS IAM Policies](https://aws.amazon.com/iam/)
* Collections of permissions to use/manage GCP resources
* Named as sercive.resource.verb
* Types:
    * Primitive roles: Owner, Editor and Viewer
    * Pre-defined roles: eg: `roles/BiGQuery.dataEditor`
    * Custom roles: 

### Cloud IAM 
Similar to [AWS IAM](https://aws.amazon.com/iam/)
* Controls access to resources, authentication
* Member is user, group, domain, service account or public.
    * Individual Google Account, Google Group, G Suite
    * Service Account belongs to application
    * Every identity has an unique e-mail address
* Policy bind members to roles at a hierarchy level: Organization -> folder -> project -> resource

### Service Account
Similar to [AWS IAM Roles](https://aws.amazon.com/iam/)
* Represents an application, not an user
* Can generate and download private keys, for non-GCP, but it's better to use Cloud Platform Managed Keys that can't be downloaded and are regenerated daily

### Cloud Identity
Similar to [AWS IAM](https://aws.amazon.com/iam/)
* Identity as a Service to provision users and groups
* Free Google Accounts for non-G-suite users
* Centrally manage al users
* MFA
* Can sync from AD and LDAP

### Security Key Enforcement
* USB or Bluetooth 2-step verification device that prevents phishing
* Eliminates Man-In-The-Middle attackas against GCP credentials

### Resource Manager
Similar to [AWS Organizations](https://aws.amazon.com/organizations/)
* Mange ans secure organization's projects with custom project hierarchy
* Define custom roles
* Apply policies at organization, folder or project level

(picture)

### Cloud Audit Logging
* Two audit logs per project and organization:
    * Admin, 400 days
    * Data access, 7 days free
    
### Cloud KMS 
Similar to [AWS KMS](https://aws.amazon.com/kms/), [Vault](https://www.vaultproject.io/)
* Low-latency service to manage & use AES256 encryption keys
* Move secrets out of code and into the environment, in a secure way
* Integrated with IAM & Cloud Audit Logging
* Rotate keys automatically or on demand

### Cloud IAP (Identity Aware Proxy)
Similar to [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
* Guards apps on GCP through identity verification instead of VPN
* Based on LB and IAM and only passes authed requests
* Grant access to any identities

### Security Scanner
Similar to [Amazon Inspector](https://aws.amazon.com/inspector/)
* GAE vulnerability scanner
* Can identify:
    * XSS
    * Flash injection
    * Mixed content (HTTP on HTTPS connection)
    * Outdated/insecure libraries
    
### Cloud DLP API (Data Loss Protection)
Similar to [AWS Macie](https://aws.amazon.com/macie/)
* Finds and optionally redacts sensitive information
* 50+ detactors: credit cards, social security number, ...


## Operations & Management

### Stackdriver
Similar to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
* Family of services for monitoring, logging and diagnosing apps

#### Stackdriver Monitoring
Similar to [CloudWatch Metrics & Dashboards](https://aws.amazon.com/cloudwatch/)
* Visibility into performance, uptime & health, based on callectd
* Basic notifies on email and GCP Mobile App
* Paid notifies on stack, SMS, websocket, ...

#### Stackdriver logging
Similar to [CloudWatch Logs](https://aws.amazon.com/cloudwatch/), [Splunk](https://www.splunk.com/)
* Store, search, analyze, monitor and alerts on logs

#### Stackdriver Error Reporting
* Counts, analyzes, tracks errors in centralized interface

#### Stackdriver Trace
Similar to [AWS X-Ray](https://aws.amazon.com/xray/), Zipkin
* Tracks and displays call tree & timing across distributed systems, to debug performance
* Generate reports
* Detect app latency shift over time

#### Stackdriver Debugger
* Grabs program state (callstack, variables, expressions) in live deployments
* Multiple view source supported

#### Deployment Manager
Similar to [AWS CloudFormation](https://aws.amazon.com/cloudformation/), Terraform
* Create/manage resources, Infrastructure as code

#### Cloud Billing API
Similar to AWS Billing API


## Development & APIs

### Cloud Source Repository
Similar to [AWS CodeCommit](https://aws.amazon.com/codecommit/)
* Private Git repository integrated with GCP
* Natural integration with Stackdriver

### Container Builder
Similar to [Amazon CodeBuild](https://aws.amazon.com/codebuild/)
* Turns code into artifacts packaged as Docker images (or anything!)

### Container Registry
Similar to [Amazon ECR](https://aws.amazon.com/ecr/)
* Based on GCS, Docker V2 registry API
* Creates & manages a multi-region GCS bucket, then GCR calls to GCS

### Cloud Endpoints
Similar to [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
* Handles authorization, monitoring, logging, API keys
* Distributed and hooked up into LB directly
* Uses JWTs, integrates with Firebase, Auth0 & Google Auth
* Can transcode HTTP JSON -> GRPC

### Apigee
Similar to [Amazon API Gateway](https://aws.amazon.com/api-gateway/) + [AWS Shield](https://aws.amazon.com/shield/)
* Full-featured API management platform 
* Transform calls between different protocols
* Authenticate via OAuth, SAML, LDAP
* Quotas and API versions
* Apigee Sense identifies suspicious API behaviours
* Apigee API Monetization supports various revenew models

### TestLab for Android
Similar to [AWS Device Farm](https://aws.amazon.com/device-farm/)
* Running test matrix across variety of real Android devices


## Links

* Architecture examples: https://gcp.solutions/
* blog: https://cloudplatform.googleblog.com
