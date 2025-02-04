# S3 and KMS Ransomware Protection

This page provides reference controls to help prevent against ransomware in AWS and to create an effective data perimeter with cloud-native controls such as encryption with KMS and IAM policies. 11 different ransomware protection cases are covered below.  Please see accompanying blog post for more detailed explanations of each control.

The controls will help prevent: 

* Unauthorized data access
* Unauthorized data deletion
* Unauthorized data corruption (encryption or modification)

For support and feedback, email <info@fogsecurity.io>

Accompanying Blog Post: [https://www.fogsecurity.io/blog/the-complete-guide-to-ransomware-protection-in-s3-and-kms](https://www.fogsecurity.io/blog/the-complete-guide-to-ransomware-protection-in-s3-and-kms)

## Control Types 

* Bucket Policies (Resource-Based Policies)
* Resource Control Policies (RCPs)
* Service Control Policies (SCPs)
* Account and Bucket Settings (Object settings as necessary)

## Ransomware Prevention Use Cases

### Prevent Customer-Provided Encryption (SSE-C)

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_s3_sse_c_encryption.json](policies/resource_control_policies)/prevent_s3_sse_c_encryption.json| RCP | RCP to block S3 SSE-C Encrpytion | organizations:CreatePolicy and organizations:AttachPolicy |
| 

### Prevent Public Access to S3 Data (General)

### Prevent Public Access to S3 (ACLs)

### Prevent Deletion of Data in S3

### Require AWS KMS Encryption (non SSE-C and non-S3 Managed)

### Prevent Modification of Account Settings

### Prevent Modification of Bucket and Object Settings

### KMS: Prevent External Access (Outside Organization) to KMS

### KMS: Prevent External Key Store (XKS)

### KMS: Prevent Key Creation with non AWS_KMS Key Material

### KMS: Prevent Key Usage with non AWS_KMS Key Material
