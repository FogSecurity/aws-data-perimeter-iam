# IAM References for Data Perimeters, Ransomware, and Data Security

Fog Security: https://www.fogsecurity.io/ 

Contact info@fogsecurity.io for help and feedback. Additions or feedback can be submitted here as well.

## Ransomware Prevention

Within this repository, we have created references to help prevent ransomware.  These controls will focus on ransomware targeting Amazon S3 and KMS.

See [ransomware protection in this repository](ransomware_protection.md) for more information and [our accompanying blog here.](https://www.fogsecurity.io/blog/the-complete-guide-to-ransomware-protection-in-s3-and-kms)

Resources:

* Resource Control Policies
* Resource-Based Policies such as Bucket Policies
* Service Control Policies
* S3 Bucket and Account Settings

## Policies

This folder contains references for managing IAM Policies.  This section will focus on AWS Organizational Policies.

* [Resource Control Policies](policies/resource_control_policies)

  Resource control policies are used to manage maximum available permissions to resources in your organization.  See [AWS Documentation](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps.html#:~:text=Resource%20control%20policies%20(RCPs)%20are,for%20resources%20in%20your%20organization.) for more information.

  We provide examples of RCPs that can be used for data perimeters and data security.
  
* [Service Control Policies](policies/service_control_policies)

  **Work in Progress**

## IAM Reference

This folder contains AWS IAM references and research.

* [AWS Service Encryption IAM Actions](iam_reference/encryption_update.md)

This research coveres IAM actions necessary to update and modify encryption on existing AWS resources.  Modifying and updating encryption is one avenue of ransomware to remove legitimate access to data.
