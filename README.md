## Terraform Import Example

### Purpose
Purpose is to try simple terraform resource import into state

### Implementation
- create s3 bucket in aws account
- create terraform configuration that represents s3 resource (e.g. main.tf => `aws_s3_bucket...`)
- initialize terraform and run appropriate import command for resource type

### Example
- let figure out a bucket name for a random employee like `john-doe-1-1-22-personal-bucket`
- run `aws s3api create-bucket --bucket john-doe-30-personal-bucket` to create s3 bucket in your account
- run `terraform init` to initialize terraform 
- run `terraform show` to see any known state resources (will return "no state")
- review existing terraform resource config (main.tf has example resource of type `aws_s3_bucket` with name `my_existing_bucket`)
- run `terraform import aws_s3_bucket.my_existing_bucket john-doe-1-1-22-personal-bucket` to identify s3 resource to import
- run `terraform show` to see any known state resources (will no show aws bucket resource "no state")

### Result
```
# aws_s3_bucket.my_existing_bucket:
resource "aws_s3_bucket" "my_existing_bucket" {
    bucket                      = "john-doe-1-1-22-personal-bucket"
    ...
    ...
```

### Requirements
- aws cli installed with permission to create s3 bucket 
- terraform installed
- terraform needs secret key and access key (fill in secrets.tf)

### Documentation
Terraform Import: https://www.terraform.io/cli/import
Terraform Import Tutorial: https://learn.hashicorp.com/tutorials/terraform/state-import?in=terraform/state&utm_source=WEBSITE&utm_medium=WEB_IO&utm_offer=ARTICLE_PAGE&utm_content=DOCS