# AWS

### Pricing
* Provisioned: to be ready to handle X load
* Usage: handle whatever I use
* Network traffic
    * Free ingress (incoming)
    * Charged egress (outgoing)

### Security
* Separation of duties and physical security
* Absolutely everything encrypted at rest
* Strong key and identity management

### Scale & automation
* Soft limits applied that can be removed/increased contacting AWS

## Services

### Compute

#### [EC2](https://aws.amazon.com/ec2/)
Similar to Compute Engine
* VM on demand
* Multiple pre-sized CPU and RAM instances
* Options:
  * On-Demand: pay per hour or seconds depending on the instance type.
  * Spot instances: up to 90% off the On-Demand price by requesting spare EC2 computing capacity. Flexible start and end times.
  * Reserved instances: up to 75% off the On-Deman price when  reserving for long term commitment, 1-3 years.

#### [EKS](https://aws.amazon.com/eks/)
Similar to [Google Kubernetes Engine]()
* Managed Kubernetes cluster with autoscaling
* Pay a fixed fee per hour for each EKS cluster + AWS Resources used under the hood (ECS, EBS)

#### [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
Similar to App Engine
* PaaS that takes code and runs it
* Autoscale (up and down) based on load
* Pay per underlying ECS instances, S3 buckets, ...

#### [Lambda](https://aws.amazon.com/lambda)
Similar to Cloud Functions
* NodeJS, Java, C# or Python code to respond to an event
* Also known as FaaS or Serverless
* Multiple Lambdas could be orchestrated using [AWS Step Functions](https://aws.amazon.com/step-functions/)
* Pay per CPU and RAM assigned per 100ms
* Gets an HTTP endpoint automatically

### Persistance

#### [Elastic Block Storage](https://aws.amazon.com/ebs/)
Similar to Google Cloud Persistent Disk
* Network attached
* Boot disk for GCE instances
* Performace scales with volume size, but slower than SSD
* Replicated for surability
* Can be resized, but still needs filesystem update in VM
* Save image snapshots

#### [Amazon RDS](https://aws.amazon.com/rds/)
Similar to Cloud SQL

#### [Amazon Athenea](https://aws.amazon.com/athena/)
Similar to Big Query

#### [DynamoDB](https://aws.amazon.com/dynamodb/)
Similar to Cloud Datastore

#### [S3](https://aws.amazon.com/s3/)
Similar to Cloud Storage

#### [AWS Snowball](https://aws.amazon.com/snow/)
Similar to Data Transfer Appliance


### Networking

#### [Amazon Route 53](https://aws.amazon.com/route53/)
Similar to Google Domains and Cloud DNS

#### [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/)

#### [CloudFront](https://aws.amazon.com/cloudfront/)

#### [Amazon VPC](https://aws.amazon.com/vpc/)

#### Cloud Interconnect
* Options for connecting external networks to Google's network
* Private connection to VPC via CloudVPN or Dedicated Interconnect (with SLAs)
* Public Google Services accesible via External Peering (No SLAs)
* Reduces egress fees

#### AWS VPN

#### [AWS DirectConnect](https://aws.amazon.com/directconnect/)


### Machine Learning

#### [Amazon Machine Learning](https://aws.amazon.com/sagemaker/)

#### [Amazon Rekognition](https://aws.amazon.com/rekognition/)

#### [Amazon Lex](https://aws.amazon.com/lex/)


### Big Data

#### [AWS IoT](https://aws.amazon.com/iot-core/)
Similar to Cloud IoT Core

#### [Amazon SNS](https://aws.amazon.com/sns/)
Similar to Cloud Pub/Sub, Kafka

#### [Amazon SQS](https://aws.amazon.com/sqs/)
Similar to Cloud Pub/Sub, Kafka

#### [AWS Glue](https://aws.amazon.com/glue/)
Similar to Cloud Data Prep

#### [Amazon EMR](https://aws.amazon.com/emr/)
Similar to Cloud Data Proc

#### [Amazon QuickSight](https://aws.amazon.com/quicksight/)
Similar to Cloud DataStudio


## Security & identity

### [AWS IAM Policies](https://aws.amazon.com/iam/)
Similar to Roles

### [AWS IAM Roles](https://aws.amazon.com/iam/)
Similar to Service Account

### [AWS IAM](https://aws.amazon.com/iam/)
Similar to Cloud Identity and Cloud IAM

### [AWS Organizations](https://aws.amazon.com/organizations/)
Similar to Resource Manager

### [AWS KMS](https://aws.amazon.com/kms/) 
Similar to Cloud KMS, [Vault](https://www.vaultproject.io/)

### [Amazon Inspector](https://aws.amazon.com/inspector/)
Similar to Security Scanner
    
### [AWS Macie](https://aws.amazon.com/macie/)
Similar to Cloud DLP API (Data Loss Protection)


## Operations & Management

### [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
Similar to StackDriver
* Family of services for monitoring, logging and diagnosing apps

#### [CloudWatch Metrics & Dashboards](https://aws.amazon.com/cloudwatch/)
Similar to Stackdriver Monitoring

#### [CloudWatch Logs](https://aws.amazon.com/cloudwatch/)
Similar to Stackdriver logging, [Splunk](https://www.splunk.com/)
* Store, search, analyze, monitor and alerts on logs

#### [AWS X-Ray](https://aws.amazon.com/xray/)
Similar to Stackdriver Trace, Zipkin

#### [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
Similar to Deployment Manager, Terraform
* Create/manage resources, Infrastructure as code


## Development & APIs

### [AWS CodeCommit](https://aws.amazon.com/codecommit/)
Similar to Cloud Source Repository

### [Amazon CodeBuild](https://aws.amazon.com/codebuild/)
Similar to Container Builder

### [Amazon ECR](https://aws.amazon.com/ecr/)
Similar to Container Registry

### [Amazon API Gateway](https://aws.amazon.com/api-gateway/)
Similar to Cloud Endpoints

### [AWS Device Farm](https://aws.amazon.com/device-farm/)
Similar to TestLab for Android
* Running test matrix across variety of real Android devices
