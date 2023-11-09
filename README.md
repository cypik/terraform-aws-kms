# Terraform-aws-kms

# AWS Infrastructure Provisioning with Terraform

## Table of Contents
- [Introduction](#introduction)
- [Usage](#usage)
- [Module Inputs](#module-inputs)
- [Module Outputs](#module-outputs)
- [License](#license)

## Introduction
This project deploys a Google Cloud infrastructure using Terraform to create aws-kms .
## Usage
To use this module, you should have Terraform installed and configured for AWS. This module provides the necessary Terraform configuration for creating AWS resources, and you can customize the inputs as needed. Below is an example of how to use this module:
## Examples

## Example: Default

```hcl
module "kms_key" {
  source                  = "git::https://github.com/opz0/terraform-aws-kms.git?ref=v1.0.0"
  name                    = "kms"
  environment             = "test"
  deletion_window_in_days = 7
  alias                   = "alias/cloudtrail_Name"
  kms_key_enabled         = true
  multi_region            = true
  valid_to                = "2023-11-21T23:20:50Z"
  policy                  = data.aws_iam_policy_document.default.json
}
```

## Example: kms-key-external
```hcl
module "kms_key" {
  source                  = "git::https://github.com/opz0/terraform-aws-kms.git?ref=v1.0.0"
  name                    = "kms"
  environment             = "test"
  deletion_window_in_days = 7
  alias                   = "alias/external_key"
  kms_key_enabled         = false
  enabled                 = true
  multi_region            = true
  create_external_enabled = true
  valid_to                = "2023-11-21T23:20:50Z"
  key_material_base64     = "WblXXXXXXXXXXXXXXXXXXXX"
  policy                  = data.aws_iam_policy_document.default.json
}
```

## Example: kms-key-replica

```hcl
module "kms_key" {
  source                  = "git::https://github.com/opz0/terraform-aws-kms.git?ref=v1.0.0"
  name                    = "kms"
  environment             = "test"
  deletion_window_in_days = 7
  alias                   = "alias/replicate_key"
  kms_key_enabled         = false
  create_replica_enabled  = true
  enabled                 = true
  multi_region            = false
  primary_key_arn         = "arn:aws:kms:us:key/XXXXXXXXXXXXXXXX"
  policy                  = data.aws_iam_policy_document.default.json
}
```

## Module Inputs
- `name`: The display name of the alias.
- `environment`: The environment for your application.
- `policy`:  A valid policy JSON document.
- For security group settings, you can configure the ingress and egress rules using variables like:

## Module Outputs
- `id` : Unique identifier for the rule.
- `tags`:  A map of tags to assign to the object.
- `arn`: The Amazon Resource Name (ARN) of the key.
- `key_id`:  The globally unique identifier for the key.
- Other relevant security group outputs (modify as needed).

## Examples
For detailed examples on how to use this module, please refer to the 'examples' directory within this repository.

## Author
Your Name Replace '[License Name]' and '[Your Name]' with the appropriate license and your information. Feel free to expand this README with additional details or usage instructions as needed for your specific use case.

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/opz0/terraform-gcp-kms/blob/master/LICENSE) file for details.
