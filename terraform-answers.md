Q1: What is the Terraform state file used for?
The Terraform state file (terraform.tfstate) tracks the current state of infrastructure that Terraform manages. It maps real-world resources to your configuration, allowing Terraform to know what exists, what needs to be created and what needs to be destroyed or updated.

Q2: Why is storing state locally risky in a team environment?
Local state is only visible to one person's machine. Team members cannot see the current state, leading to conflicts, duplicate resources or accidental destruction of infrastructure. There is also no locking mechanism, meaning two people could run Terraform simultaneously and corrupt the state file.

Q3: What is a remote backend?
A remote backend stores the Terraform state file in a shared, centralized location such as AWS S3 instead of locally. This allows teams to share state, enables state locking to prevent conflicts and keeps sensitive infrastructure data off individual machines.

Q4: Example S3 Remote Backend Block:
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "project/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock-table"
    encrypt        = true
  }
}
