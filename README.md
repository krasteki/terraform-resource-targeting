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

II. Target specific bucket objects

1. Update `main.tf` contents of the bucket objects.
```
resource "aws_s3_bucket_object" "objects" {
    ###
-  content      = "Example object #${count.index}"
+  content      = "Bucket object #${count.index}"
    ###
}
```
2. Apply this change to two of the bucket objects. Confirm with a `yes`
```
$ terraform apply -target="aws_s3_bucket_object.objects[2]" -target="aws_s3_bucket_object.objects[3]"
```

III. Target bucket object names

1. Remove the `prefix` argument from the `random_pet.object_names` resource in `main.tf`.

2. apply the config and confirm `yes`
```
$ terraform apply -target="aws_s3_bucket_object.objects[2]"
```
Terraform updated all five of the names because the entire `aws_s3_bucket_objects.objects` resource depends on the entire `random_pet.object_names`

IV. Destroy your infrastructure

1. Terraform's destroy command also accepts resource targeting.
```
$ terraform destroy -target="aws_s3_bucket_object.objects"
```

2. Destroy the rest of the infrastructure 

```
$ terraform destroy
```