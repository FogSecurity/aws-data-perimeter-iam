# IAM Policies for AWS KMS Data Protection

**Work in Progress**

This folder contains useful AWS IAM Policies to help with data security.  

Use cases include:
* Preventing unauthorized usage of unapproved encryption mechanisms.
* Protecting against ransomware attacks.
* Ensuring access to encryption keys.
* Safeguarding KMS Keys.

These policies can either be used as:
* IAM Managed Policies
* Service Control Policies (SCPs).

Note: these policies are written as 'deny' statements as to block actions.  Policies may also be written as 'allow' statements.  Due to the evaluation of IAM policies, 'deny' statements will prevent actions even if they are allowed at other levels.  'Allow' statements may not 'deny' unwanted actions.

Comments, questions, information, and help with cloud data security can be directed to info@fogsecurity.io.

## Policies Included in Folder

### Deny Custom Key Store
* Filename: deny_custom_key_store.json

### Deny Key Creation with non AWS KMS Key Material

### Deny External Key Material Import

### Deny Key Lockout

### AWS References
* [AWS Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
