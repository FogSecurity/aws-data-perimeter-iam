# Resource Control Policies

Fog Security: https://www.fogsecurity.io/ 

Accompanying Blog Post: https://www.fogsecurity.io/blog/data-perimeters-with-resource-control-policies-and-aws-kms

Contact info@fogsecurity.io for help and feedback. Additions or feedback can be submitted here as well.


## Resource Control Policies

Resource Control Policies are a newer type of AWS Organizations policy released in November of 2024 that control maximum permissions for resources in your organization.  These offer a central and scaleable way of managing resources.  These differ from Service Control Policies (SCPs).  SCPs control actions that IAM principals under one's management can perform, while RCPs control actions that can be performed on resources under one's management (resources within the Organization). 

Below, we have example policies that can be used to create data perimeters and protect resources in your organization.  As with any policy, we recommend thorough testing prior to applying any policy.

## Policies

#### Encryption Perimeter (Data Read)
File: [encryption_read_perimeter.json](encryption_read_perimeter.json)

This policy restricts access by denying `kms:Decrypt` to principals outside of your organization.  If using AWS KMS CMKs to encrypt data, this policy helps with protecting data across any service that utilizes KMS from unintended outside access.

#### Prevent KMS Key Lockout
File: [prevent_kms_key_lockout.json](prevent_kms_key_lockout.json)

This policy ensures that no KMS Key is created with a KMS Key policy (resource-based policy) that locks out management.  Unlocking these malformed KMS key policies typically required AWS support or leveraging account root credentials (and now can be done via `AssumeRoot`).  However, we recommend preventing situations that require elevated access.

#### Production Data Restriction
File: [production_data_restrict.json](production_data_restrict.json)

In scenarios where an Organization is organized with Organization Units that represent Production and different environments, this policy can help with preventing cross-environment data access.  In some cases, access to Production data from lower environments such as Development or Sandbox may be unwanted.  This policy uses Organization Paths (OUs) to prevent cross-environment access.

#### Protect Secrets and Ensure Secrets are Non-Public
File: [protect_secrets_nonpublic.json](protect_secrets_nonpublic.json)

This RCP provides 2 layers of security for secrets in Secrets Manager:
* Denies access to the resource if it comes from outside of the Organization.
* Denies access to create public resource policies on a Secret via the `secretsmanager:BlockPublicPolicy` condition key.

#### Require KMS Encryption for any object uploaded to S3
File: [require_kms_encryption.json](require_kms_encryption.json)

This RCP requires any upload via `s3:PutObject` or `s3:ReplicateObject` to require KMS encryption.  
