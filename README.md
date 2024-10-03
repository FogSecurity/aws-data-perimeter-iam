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

### AWS Service Encryption IAM Actions Table

| AWS Service | IAM Action | Action Description | Access Level (AWS) | Dependent Actions | Data Access Level |
| ------------- | ----------- | ------------- | ------------------ | ------------------ | ------------------ | 
| S3 (Simple Storage Service) | s3:PutEncryptionConfiguration | Grants permission to set the encryption configuration for an Amazon S3 bucket | Write | - | Create/Update |
| DynamoDB | dynamodb:UpdateTable | Grants permission to modify the provisioned throughput settings, global secondary indexes, or DynamoDB Streams settings for a given table | Write | - | Create/Update |


### WS Service Encryption IAM Actions Table (Creation of Resources, Encryption Secondary)
| AWS Service | IAM Action | Action Description | Access Level (AWS) | Dependent Actions | Data Access Level |
| ------------- | ----------- | ------------- | ------------------ | ------------------ | ------------------ | 
| S3 (Simple Storage Service) | s3:PutObject | Grants permission to add an object to a bucket | Write | - | Create |
| S3 (Simple Storage Service) | s3:CreateJob | Grants permission to create a new Amazon S3 Batch Operations job | Write | - | Create |
| DynamoDB | dynamodb:CreateTable | Grants permission to the CreateTable operation adds a new table to your account | Write | - | Create |


## Reference Policies

This folder contains helpful AWS IAM Policies for AWS Encryption Management


