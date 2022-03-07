# Learn Terraform Resource Targeting

Learn what Terraform resource targeting is and how to use it.

Follow along with the [Learn
tutorial](https://learn.hashicorp.com/tutorials/terraform/resource-targeting?in=terraform/state)
at HashiCorp Learn.

This repository implements an S3 bucket and bucket objects.

I. Target the S3 bucket name

1. In `main.tf`, replace the value of `random_pet.bucket_name` resource from 3 to 5, plan the change.

2. Plan the change again, but only target the `random_pet.bucket_name` resource.
```
$ terraform plan -target="random_pet.bucket_name"
```
Terraform will apply the change to all resources in the `module`. Target the S3 bucket module.
```
$ terraform plan -target="module.s3_bucket"
```
3. Change the output `bucket_name` to refer to the bucket name directly.
4. Apply the config
```
$ terraform apply
```
