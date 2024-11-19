# IAM References for AWS KMS Encryption: Updating Encryption on AWS Data Resources

Fog Security: https://www.fogsecurity.io/ \
Accompanying Blog Post: https://www.fogsecurity.io/blog/updating-encryption-in-aws-ransonware

Contact info@fogsecurity.io for help and feedback. Additions or feedback can be submitted here as well.

## Overview

With ransomware on the rise, we look at one of the crucial attack vectors of ransomware: re-encrypting or encrypting cloud data resources.  Access in AWS cloud is governed by AWS Identity and Access Management and re-encrypting cloud data resources requires specific cloud permissions.  In order for an attacker to perform ransomware where data is re-encrypted with a encryption key that the attacker controls, these IAM permissions to update encryption or delete data resources are required.

We found the following across 65 resources pver 45 AWS services:
* 24 resources across 18 services had support for updating encryption via IAM methods.
* 41 resources across 27 services could not have encryption updated and would require recreation.

## AWS Service Encryption IAM Actions 

This section covers service-specific actions to set and update encryption options on AWS resources.  For example, setting S3 encryption for a bucket or updating a DynamoDB's encryption setting. 

Unauthorized use of these actions can lead to:
* Ransonware
* Data access issues
* Application availability issues
* Misconfiguration of data

There are authorized use of these actions with some reasons below:
* Update to security guardrails that require changes to different encryption keys.
* Switching encryption from types of encryption keys such as to CMKs from AWS Owned or AWS Managed.
* Standard maintenance or update of application and data encryption.
* Data ownership team change.

See [blog post](https://www.fogsecurity.io/blog/updating-encryption-in-aws-ransonware) for more insights from our research.

### AWS Service Encryption IAM Actions Table (Update Resources)

| AWS Service | AWS Resource| IAM Action | Action Description | Access Level (AWS) | Encryption Only |
| ------------- | ----------- | ------------- | ------------------ | ------------------ | ------------ |
| DynamoDB | DynamoDB Table | dynamodb:UpdateTable | Grants permission to modify the provisioned throughput settings, global secondary indexes, or DynamoDB Streams settings for a given table | Write | No |
| SQS | Queue | sqs:SetQueueAttributes | Grants permission to set the value of one or more queue attributes | Write | No |
| Secrets Manager | Secret | secretsmanager:updateSecret | Grants permission to update a secret with new metadata or with a new version of the encrypted data | Write | No |
| Glue | Glue Data Catalog Metadata | glue:PutDataCatalogEncryptionSettings | Grants permission to update catalog encryption settings | Write | Yes | 
| Glue | Glue Data Catalog Connection Passwords | glue:PutDataCatalogEncryptionSettings | Grants permission to update catalog encryption settings | Write | Yes | 
| QLDB | Ledger | qldb:updateLedger | 	Grants permission to update properties on a ledger | Write | No |
| Lambda | Lambda Environment Variables | lambda:UpdateFunctionConfiguration | Grants permission to modify the version-specific settings of an AWS Lambda function | Write | No |
| Redshift | Redshift Cluster | redshift:ModifyCluster | Grants permission to modify the settings of a cluster | Write | No |
| RDS | RDS Instance Master User Secret | rds:ModifyDBInstance | Grants permission to modify settings for a DB instance | Write | No |
| RDS | RDS Instance Performance Insights | rds:ModifyDBInstance | Grants permission to modify settings for a DB instance | Write | No |
| RDS | RDS Cluster Master User Secret | rds:ModifyDBCluster| Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster | Write | No |
| RDS | RDS Cluster Performance Insights | rds:ModifyDBCluster | Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster |Write | No |
| RDS | RDS Cluster Storage Encryption | rds:ModifyDBCluster | Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster | Write | No |
| Redshift Serverless | Namespace | redshift-serverless:UpdateNamespace | Grants permission to update a namespace with the specified configuration settings | Write | No |
| Keyspaces (Cassandra) | Table | cassandra:alter | Grants permission to alter a keyspace or table | Write | No |
| Timestream | Timestream Database | timestream:UpdateDatabase | Grants permission to update a database in your account | Write | Yes |
| Timestream | Timestream Table Magnetic Store (S3) | timestream:UpdateTable | Grants permission to update a table in your account | Write | No |
| Simple Notification Service (SNS) | SNS Topic | sns:SetTopicAttributes | Grants permission to allow a topic owner to set an attribute of the topic to a new value | Permissions Management | No |
| CloudWatch | CloudWatch Log Group | logs:AssociateKMSKey | Grants permission to associate the specified AWS Key Management Service (AWS KMS) customer master key (CMK) with the specified log group | Write | Yes |
| Kinesis | Firehose Stream | firehose:StartDeliveryStreamEncryption | Grants permission to enable server-side encryption (SSE) for the delivery stream | Write | Yes |
| X-Ray | Trace | xray:PutEncryptionConfig | Grants permission to update the encryption configuration for X-Ray data | Permissions Management | Yes |
| OpenSearch | OpenSearch Domain | es:UpdateDomainConfig | Grants permission to modify the configuration of an OpenSearch Service domain, such as the instance type or number of instances | Write | No |
| CodeCommit | CodeCommit Repository | codecommit:UpdateRepositoryEncryptionKey | Grants permission to change the AWS KMS encryption key used to encrypt and decrypt an AWS CodeCommit repository | Write | Yes |
| EMR Serverless | EMR Serverless Application Managed Logs |  emr-serverless:UpdateApplication | Grants permission to Update an application | Write | No |

Interesting Notes:
* Timestream Update Database only updates encryption settings: https://docs.aws.amazon.com/timestream/latest/developerguide/API_UpdateDatabase.html
* PII Entities Detection Job in Comprehend does not have the ability to specify Volume KMS Key ID.

## AWS Resources that cannot have encryption updated directly (only on creation)

| AWS Service | AWS Resource |
| ------------- | ----------- |
| SSM Parameter Store | SecureString Parameter |
| S3 (Simple Storage Service) | S3 Bucket |
| RDS | RDS Database Instance |
| EFS | EFS File System | 
| Aurora | Aurora Database Instance |
| ElastiCache | Global Datastore (Cluster) |
| ElastiCache | Redis Cache |
| ElastiCache | Memcached Cache | 
| ElastiCache | Serverless Cache |
| MemoryDB | MemoryDB Cluster | 
| Neptune | Neptune Cluster | 
| Neptune | Neptune Instance | 
| Elastic Block Store (EBS) | EBS Volume |
| Lightsail | Lightsail Managed DB |
| Location Service | Location Trackers |
| Location Service | Location Geofence Collection | 
| Prometheus | Workspace | 
| Managed Streaming for Apache Kafka | MSK Cluster |
| Sagemaker | Sagemaker Notebook Instance |
| Comprehend | Document Classification Job Volume |
| Comprehend | Entities Detection Job Volume |
| Comprehend | Topics Detection Job Volume |
| Comprehend | Targeted Sentiment Detection Job Volume |
| Comprehend | Sentiment Detection Job Volume |
| Comprehend | Key Phrases Detection Job Volume |
| Comprehend | Dominant Language Detection Job Volume |
| Amazon MQ | ActiveMQ Broker |
| Amazon MQ | RabbitMQ Broker |
| Kendra | Kendra Index |
| Elastic Container Registry (ECR) | ECR Repository | 
| Database Migration Service (DMS) | Replication Instance | 
| Kinesis Video | Kinesis Video Stream |
| FSx | File System |
| FSx | File Cache |
| AppFlow | Flow |
| AppFlow | Connector Profile | 
| DynamoDB Accelerator (DAX) | DAX Cluster |
| CodeArtifact | CodeArtifact Domain |
| Healthlake | Healthlake Datastore |
| Managed WorkFlows for Apache Airflow (MWAA) | MWAA Environment |
| Amazon Q | Amazon Q Business Application |

## Unencrypted Resources

| AWS Service | AWS Resource |
| ------------- | ----------- |
| SSM Parameter Store | String Parameter |
| SSM Parameter Store | StringList Parameter |

* S3 is included in AWS Resources that cannot have encryption updated directly as changing bucket level encryption does not change the encryption settings for existing objects in the S3 bucket.

## Encryption Settings 
| AWS Service | AWS Resource | IAM Action | Action Description | Access Level (AWS) |
| ------------- | ----------- | ----------- | ----------- | ----------- | 
| S3 (Simple Storage Service) | S3 Bucket | s3:PutEncryptionConfiguration | Grants permission to set the encryption configuration for an Amazon S3 bucket | Write |
| OpenSearch Serverless | OpenSearch Collection | aoss:CreateSecurityPolicy | Grants permission to create a network or encryption policy | Write |
| OpenSearch Serverless | OpenSearch Collection | aoss:UpdateSecurityPolicy | Grants permission to update a security policy | Write |
