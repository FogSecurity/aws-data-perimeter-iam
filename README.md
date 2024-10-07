# IAM References for AWS KMS Encryption

Fog Security: https://www.fogsecurity.io/
Accompanying Blog Post: TBD

Contact info@fogsecurity.io for help and feedback. Additions or feedback can be submitted here as well.

## Overview

## AWS Service Encryption IAM Actions 

This section covers service-specific actions to set and update encryption options on AWS resources.  For example, setting S3 encryption for a bucket or updating a DynamoDB's encryption setting. 

Unauthorized use of these actions can lead to:
* Ransonware
* Data access issues
* Application availability issues
* Misconfiguration of data

### AWS Service Encryption IAM Actions Table (Update Resources)

| AWS Service | AWS Resource| IAM Action | Action Description | Access Level (AWS) | Encryption Only |
| ------------- | ----------- | ------------- | ------------------ | ------------------ | ------------ |
| DynamoDB | DynamoDB Table | dynamodb:UpdateTable | Grants permission to modify the provisioned throughput settings, global secondary indexes, or DynamoDB Streams settings for a given table | Write | No |
| SQS | Queue | sqs:SetQueueAttributes | Grants permission to set the value of one or more queue attributes | Write | No |
| Secrets Manager | Secret | secretsmanager:updateSecret | Grants permission to update a secret with new metadata or with a new version of the encrypted data | Write | No |
| Glue | Glue Data Catalog | glue:PutDataCatalogEncryptionSettings | Grants permission to update catalog encryption settings | Write | Yes | 
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



Interesting Notes:
* Timestream Update Database only updates encryption settings: https://docs.aws.amazon.com/timestream/latest/developerguide/API_UpdateDatabase.html


## AWS Resources that cannot have encryption updated directly (only on creation)

| AWS Service | AWS Resource |
| ------------- | ----------- |
| SSM Parameter Store | SecureString Parameter |
| S3 (Simple Storage Service) | S3 Bucket |
| RDS | RDS Database Instance |
| EFS | EFS File System | 
| ElastiCache | Global Datastore (Cluster) |
| Aurora | Aurora Database Instance |
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

## Unencrypted Resources

| AWS Service | AWS Resource |
| ------------- | ----------- |
| SSM Parameter Store | String Parameter |
| SSM Parameter STore | StringList Parameter |

* S3 is included in AWS Resources that cannot have encryption updated directly as changing bucket level encryption does not change the encryption settings for existing objects in the S3 bucket.

## Encryption Settings 
| AWS Service | IAM Action | Action Description | Access Level (AWS) |
| ------------- | ----------- | ----------- | ----------- | 
| S3 (Simple Storage Service) | s3:PutEncryptionConfiguration | Grants permission to set the encryption configuration for an Amazon S3 bucket | Write |

## Reference Policies

This folder contains helpful AWS IAM Policies for AWS Encryption Management


