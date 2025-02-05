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
| [prevent_s3_sse_c_encryption.json](policies/resource_control_policies/prevent_s3_sse_c_encryption.json)| RCP | RCP to block S3 SSE-C Encryption | organizations:CreatePolicy and organizations:AttachPolicy |
| [prevent_s3_sse_c_encryption.json](policies/bucket_policies/prevent_s3_sse_c_encryption.json) | Bucket Policy | Bucket Policy to block S3 SSE-C Encryption | s3:PutBucketPolicy |

### Prevent Public Access to S3 Data (General)

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_public_s3.json](policies/resource_control_policies/prevent_public_s3.json)| RCP | RCP to block access to S3 from outside organization | organizations:CreatePolicy and organizations:AttachPolicy |
| See below code snippet | Account Setting | Set Account Public Access Block | s3:GetAccountPublicAccessBlock and s3:PutAccountPublicAccessBlock | 

```
aws s3control put-public-access-block \
--account-id <your_account_here> \
--public-access-block-configuration '{"BlockPublicAcls": true, "IgnorePublicAcls": true, "BlockPublicPolicy": true, "RestrictPublicBuckets": true}'
```

### Prevent Public Access to S3 (ACLs)

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| See below code snippet | Bucket Setting | Set Bucket Ownership Settings (and ACL settings) | s3:GetBucketOwnershipControls and s3:PutBucketOwnershipControls |

```
aws s3api put-bucket-ownership-controls \
--bucket <your_bucket_here> \
--ownership-controls="Rules=[{ObjectOwnership=BucketOwnerEnforced}]"
```

### Prevent Deletion of Data in S3

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_s3_data_delete.json](policies/bucket_policies/prevent_s3_data_delete.json)| Bucket Policy | Bucket Policy to prevent data deletion in s3 bucket | s3:PutBucketPolicy |
| See below code snippet (1) | Bucket Setting | Enable Bucket Versioning | s3:PutBucketVersioning | 
| See below code snippet (2) | Bucket Setting | Set Object Lock Mode on Bucket | s3:PutBucketObjectLockConfiguration | 

1.  Set Bucket Versioning
```
aws s3api put-bucket-versioning \
--bucket <your_bucket_here> \
--versioning-configuration Status=Enabled
```

2.  Set Object Lock
```
aws s3api put-object-lock-configuration \
--bucket <your_bucket_here> \
--object-lock-configuration='{ "ObjectLockEnabled": "Enabled", "Rule": { "DefaultRetention": { "Mode": "GOVERNANCE", "Days": 30 }}}'
```

### Require AWS KMS Encryption (non SSE-C and non-S3 Managed)

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_non_kms_encryption.json](policies/resource_control_policies/prevent_non_kms_encryption.json)| RCP | RCP to prevent non AWS KMS Encryption | organizations:CreatePolicy and organizations:AttachPolicy |
| [prevent_non_kms_encryption.json](policies/bucket_policies/prevent_non_kms_encryption.json) | Bucket Policy | Bucket Policy to prevent non AWS KMS Encryption | s3:PutBucketPolicy |

### Prevent Modification of Account Settings

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_s3_account_setting_mod.json](policies/service_control_policies/prevent_s3_account_setting_mod.json)| SCP | SCP to prevent modification of s3 account settings | organizations:CreatePolicy and organizations:AttachPolicy |

### Prevent Modification of Bucket and Object Settings

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_s3_resource_setting_mod.json](policies/resource_control_policies/prevent_s3_resource_setting_mod.json)| RCP | RCP to prevent modification of s3 bucket and object settings | organizations:CreatePolicy and organizations:AttachPolicy |

### KMS: Prevent External Access (Outside Organization) to KMS

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [encryption_read_perimeter.json](policies/resource_control_policies/encryption_read_perimeter.json)| RCP | RCP to prevent KMS decryption access from outside AWS organization | organizations:CreatePolicy and organizations:AttachPolicy |

### KMS: Prevent External Key Store (XKS)

| File Name | Control Type | Description | Permissions Needed |
|-----------|--------------|--------------|-------------------|
| [prevent_xks.json](policies/service_control_policies/prevent_xks.json)| SCP | SCP to prevent KMS external key store administration | organizations:CreatePolicy and organizations:AttachPolicy |

### KMS: Prevent Key Creation with non AWS_KMS Key Material

### KMS: Prevent Key Usage with non AWS_KMS Key Material
