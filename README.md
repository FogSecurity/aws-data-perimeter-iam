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

| AWS Service | AWS Resource| IAM Action | Action Description | Access Level (AWS) | 
| ------------- | ----------- | ------------- | ------------------ | ------------------ |
| DynamoDB | DynamoDB Table | dynamodb:UpdateTable | Grants permission to modify the provisioned throughput settings, global secondary indexes, or DynamoDB Streams settings for a given table | Write |
| SQS | Queue | sqs:SetQueueAttributes | Grants permission to set the value of one or more queue attributes | Write |
| Secrets Manager | Secret | secretsmanager:updateSecret | Grants permission to update a secret with new metadata or with a new version of the encrypted data | Write |
| Glue | Glue Data Catalog | glue:PutDataCatalogEncryptionSettings | Grants permission to update catalog encryption settings | Write |
| QLDB | Ledger | qldb:updateLedger | 	Grants permission to update properties on a ledger | Write |
| Lambda | Lambda Environment Variables | lambda:UpdateFunctionConfiguration | Grants permission to modify the version-specific settings of an AWS Lambda function | Write |
| Redshift | Redshift Cluster | redshift:ModifyCluster | Grants permission to modify the settings of a cluster | Write |
| RDS | RDS Instance Master User Secret | rds:ModifyDBInstance | Grants permission to modify settings for a DB instance | Write |
| RDS | RDS Instance Performance Insights | rds:ModifyDBInstance | Grants permission to modify settings for a DB instance | Write |
| RDS | RDS Cluster Master User Secret | rds:ModifyDBCluster| Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster | Write |
| RDS | RDS Cluster Performance Insights | rds:ModifyDBCluster | Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster |Write |
| RDS | RDS Cluster Storage Encryption | rds:ModifyDBCluster | Grants permission to modify a setting for an Amazon Aurora DB cluster or Amazon DocumentDB cluster | Write |

## AWS Resources that cannot have encryption updated directly

| AWS Service | AWS Resource |
| ------------- | ----------- |
| SSM Parameter Store | SecureString Parameter |
| S3 (Simple Storage Service) | S3 Bucket |
| RDS | RDS Database Instance |
| EFS | EFS File System | 

* S3 is included in AWS Resources that cannot have encryption updated directly as changing bucket level encryption does not change the encryption settings for existing objects in the S3 bucket.

## Encryption Settings 
| AWS Service | IAM Action | Action Description | Access Level (AWS) |
| ------------- | ----------- | ----------- | ----------- | 
| S3 (Simple Storage Service) | s3:PutEncryptionConfiguration | Grants permission to set the encryption configuration for an Amazon S3 bucket | Write |

## Reference Policies

This folder contains helpful AWS IAM Policies for AWS Encryption Management


