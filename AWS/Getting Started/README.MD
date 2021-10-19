# AWS Getting Started

## Author

 Intellipaat

## Course url

<https://www.youtube.com/watch?v=MmsoIcYrXJU>

## Cloud computing Models

![Cloud computing Models](images/cloud-computing-models.png)

### Deployment Models

- Public Cloud - Provided over the Internet and can be bought by anyone and shared.
- Private Cloud - Provisioned over private IT infrastructure for dedicated use of a single organization.
- Hybrid Cloud - A mix of on-premises, private cloud and third-party, public cloud services with orchestration between platforms.

### Service Models

- IAAS : Infrastructure as a Service
![IAAS](images/IAAS.png)

- PAAS : Platform as a Service
  ![PAAS](images/PAAS.png)

- SAAS : Software as a Service
  ![SAAS](images/SAAS.png)

## Intro to AWS

Been in the game since 2006 and has over 35% of the cloud market share.

### Service Domains in AWS

![service domains in aws](images/service-domains-in-aws.png)

#### Compute

![compute](images/aws-compute-ecosystem.png)

- EC2 : Elastic Compute Cloud is a raw server or an IAAS we get allowing us to configure whatever we wish to use ex: Database, web etc ...
- Elastic Beanstalk : Is an specialized version of EC2 which is a PAAS, which only allows for us to launch and run a web server/application.
  ![elastic beanstalk](images/elastic-beanstalk.png)
- AWS Lambda : Is another specialized version of an EC2 and is a PAAS, where we get to run backend processing on a serveless architecture
  ![AWS lambda](images/aws-lambda.png)
- AWS LoadBalancer : distribuutes incoming application or network traffic across multiple targets, such as Amazon EC2 instance, containers, and IP addresses, in multiple Availability Zones
![Elastic loadbalancer](images/elastic-loadbalancer.png)
- AWS Auto Scaling : monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost. It always have to work with in conjunction with the AWS loadbalancer.
![Auto Scaling](images/aws-auto-scaling.png)
- AWS ECR : Amazon Elastic Container Registry is a fully-managed Docker container registry that makes it easy for developers to store, manage and deploy Docker container images, simillar to dockerhub.
- AWS ECS : Amazon Elastic Container Service is a higly scalable, high-performance container orchestration servie that supports Docker containers and allows you to easily run and scale containerized application on AWS.

#### Storage

![Amazon Services Storage](images/amazon-services-storage.png)

- Amazon S3 : Amazon Simple Storage Service is an object storage service that offers industry-leading scalability, data-availability, security and performance.
  ![Sclaing](images/amazon-simple-storage-service.png)
- Amazon Glacier : is a secure, durable, and extremely low-cost cloud storage service for data archiving and long-term backup. Used to take backups of S3 buckets and manage them, usually used as a backup service.
  ![glacier](images/amazon-s3-glacier.png)
- Amazon EFS : Elastic File System is a network drive which can mount to an EC2 and handle uploads as if it were doing it on a local drive, but has the benefit or being shared and instantly available for all the other users of the app.
  ![EFS](images/amazon-efs.png)
- AWS Storage Gateway : Connects on-premise software appliance with cloud based storage to provide seamless integration with data security features between your on-premise software and the AWS storage infrastructure.
  ![Storage Gateway](images/aws-storage-gateway.png)

### Database

![Database](images/amazon-services-database.png)

- Amazon RDS : Relation Database Service makes it easy to set up, operate, and scale a relational database in the cloud.
  ![RDS](images/amazon-rds.png)
- DyamoDB : is a key-value and document database that delivers single-digit millisecond performance scale, think firebase but created by Amazon.
  ![Dynamo DB](images/dynamo-db.png)
- Amazon RedShift : Is a data warehouse provided by amazon, which comprises of multiple databases and provides and interface which can be used to analyze your data warehouse and data lake.
  ![RedShift](images/redshift.png)
- ElastiCache : Think of something like Redis which is a cache between the server and the client
  ![ElastiCache](images/elasticache.png)

#### Security

![AWS Security](images/aws-security.png)

- IAM : AWS Identity and Access Management enables you to manage access to AWS services and resources securely. This can be used to authenticate uses who will be able to configure and access the cloud servies as well as apps which will then be able to access the cloud resources like an app requiring access to the s3 bucket.
  ![IAM](images/aws-security-iam.png)

- AWS KMS : Key Management Service makes it easy for you to create and manage keys and control use of encryption across a wide range of AWS services.
![KMS](images/aws-security-kms.png)

#### Management

![Management](images/aws-services-management.png)

- AWS CloudFormation : provides a common language for you to describe and provision all the infrastructure resources in your cloud environment. This is bascially infrastructure as code in a gist, it is used to templatize an AWS Architecture Infrastructure like creating setting up a s3 bucket, creating a DB etc...
  ![Cloud Formation](images/aws-management-cloudformation.png)
- AWS OpsWorks : is a configuration management service that provides managed instances of Chef and Puppet. Chef & Puppet are automation platforms. Think of it like Cloudformation but built in a layered style like docker using Chef and Puppet
  ![OpsWorks](images/aws-management-opsworks.png)
- AWS CloudTrail : is a service that enable governanance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log continously monitor, and retain account activity related to actions your AWS infrastructure.
  ![Cloud trail](images/aws-cloud-trail.png)
- AWS CloudWatch : is a monitoring and management service built for devs, sys ops, site reliabilty engineers to configure real time alarm on the AWS resources and act on the alarms like notifying the relevant people or creating new architecture to handle the resiliency.
  ![cloud watch](images/aws-cloud-watch.png)

#### Customer Engagement

![Customer Engagement](images/amazon-services-customer-engagement.png)

- Amazon Connect : to setup customer support for companies, it takes less than 5 minutes to get customer support.
  ![Connect](images/aws-connect.png)
- Simple Email : is a cloud based email sending service designed to help digital marketers and app developers send markertng, notification and trasactional mails.
  ![Simple Email](images/aws-simple-email-service.png)

#### App Integration

![App Integration](images/app-integration.png)

- Simple Notification Service : SNS is a highly available, durable, secure, fully managed pub/sub messaging service that enables you to decouple microservices, distributed systems and serveless apps.
  ![SNS](images/aws-sns.png)
- Simple Queue Service
