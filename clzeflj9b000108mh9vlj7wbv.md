---
title: "Automating AWS EC2 Deployment with Terraform and GitLab CI/CD"
datePublished: Sat Aug 03 2024 17:52:33 GMT+0000 (Coordinated Universal Time)
cuid: clzeflj9b000108mh9vlj7wbv
slug: automating-aws-ec2-deployment-with-terraform-and-gitlab-cicd
tags: aws, devops, gitlab, terraform

---

### Introduction

This blog provides a comprehensive guide to automate AWS EC2 deployments using Terraform and GitLab CI/CD, with an added focus on storing the Terraform state file in an S3 bucket for centralized state management. We will create a pipeline that validates, plans, applies, and destroys AWS resources, ensuring a smooth and efficient deployment process. 🚀

### Prerequisites

Before we get started, make sure you have the following:

* An AWS account with access keys.
    
* A GitLab account.
    
* Basic knowledge of Terraform and GitLab CI/CD.
    

### Terraform Configuration

First, let's create our Terraform configuration files to define the AWS EC2 instance and the security group.

#### [`main.tf`](http://main.tf)

```plaintext
provider "aws" {
  region = "us-west-2"  # Replace with your desired region
}

terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"  # Replace with your bucket name
    key            = "path/to/terraform.tfstate"  # Replace with your desired state file path
    region         = "us-west-2"  # Replace with your bucket's region
    dynamodb_table = "terraform-lock-table"  # Replace with your DynamoDB table name
    encrypt        = true
  }
}

resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "example-vpc"
  }
}

resource "aws_subnet" "example" {
  vpc_id     = aws_vpc.example.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "example-subnet"
  }
}

resource "aws_security_group" "example" {
  name        = "example-security-group"
  description = "Example security group"
  vpc_id      = aws_vpc.example.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "example-security-group"
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with a valid AMI ID for your region
  instance_type = "t2.micro"

  subnet_id                   = aws_subnet.example.id
  vpc_security_group_ids      = [aws_security_group.example.id]
  associate_public_ip_address = true

  tags = {
    Name = "example-instance"
  }
}
```

### GitLab CI/CD Pipeline

Next, let's set up our GitLab CI/CD pipeline. This pipeline will validate, plan, apply, and destroy our Terraform configuration.

#### `.gitlab-ci.yml`

```yaml
stages:
  - validate
  - plan
  - apply
  - destroy

image:
  name: hashicorp/terraform:light
  entrypoint:
    - '/usr/bin/env'
    - 'PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'

variables:
  TF_IN_AUTOMATION: "true"

before_script:
  - export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY}
  - export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
  - terraform --version
  - terraform init

Terraform_validate:
  stage: validate
  script:
    - terraform validate

Terraform_plan:
  stage: plan
  script:
    - terraform plan -out=tfplan
  artifacts:
    paths:
      - tfplan
      - terraform.tfstate
      - terraform.tfstate.backup
    expire_in: 1 hour  # Adjust expiration as needed

Terraform_apply:
  stage: apply
  script:
    - terraform apply -auto-approve tfplan
  dependencies:
    - Terraform_plan
  artifacts:
    paths:
      - terraform.tfstate
      - terraform.tfstate.backup
    expire_in: 1 hour  # Adjust expiration as needed

Terraform_destroy:
  stage: destroy
  script:
    - terraform init
    - terraform destroy -auto-approve
  when: manual
  dependencies:
    - Terraform_apply
  artifacts:
    paths:
      - terraform.tfstate
      - terraform.tfstate.backup
    expire_in: 1 hour  # Adjust expiration as needed
```

### Explanation

1. **Backend Configuration**: The `terraform` block in [`main.tf`](http://main.tf) configures the backend to use S3 for storing the state file and DynamoDB for state locking.
    
2. **Pipeline Configuration**: The `.gitlab-ci.yml` file initializes Terraform and uses the S3 backend configuration.
    

### Adding AWS Credentials to GitLab CI/CD

To securely store and use your AWS credentials in your GitLab CI/CD pipeline, you need to add them as environment variables in your GitLab project settings.

**Steps to Add AWS Credentials:**

1. **Navigate to Project Settings**:
    
    * Go to your GitLab project.
        
    * Click on Settings &gt; CI/CD &gt; Variables.
        
2. **Add AWS Access Key ID**:
    
    * Click on Add Variable.
        
    * Set Key to AWS\_ACCESS\_KEY\_ID.
        
    * Set Value to your AWS Access Key ID.
        
    * Check the Protected and Masked checkboxes.
        
    * Click Add Variable.
        
3. **Add AWS Secret Access Key**:
    
    * Click on Add Variable.
        
    * Set Key to AWS\_SECRET\_ACCESS\_KEY.
        
    * Set Value to your AWS Secret Access Key.
        
    * Check the Protected and Masked checkboxes.
        
    * Click Add Variable.
        

### Running the Pipeline

1. **Initialize Terraform**:
    
    ```bash
    terraform init
    ```
    
2. **Commit and Push**: Commit your updated [`main.tf`](http://main.tf) and `.gitlab-ci.yml` files to your GitLab repository and push the changes.
    
3. **Pipeline Execution**: Navigate to your GitLab project and go to CI/CD &gt; Pipelines. You should see your pipeline running through the defined stages.
    

### Conclusion

By storing the Terraform state file in an S3 bucket and using DynamoDB for state locking, we enhance the reliability and security of our infrastructure management process. This setup, combined with GitLab CI/CD, provides a robust and scalable solution for automating AWS resource deployments. 🌟

#DevOps #Terraform #AWS #GitLabCI #Automation #CloudComputing #InfrastructureAsCode #S3 #DynamoDB

---

Feel free to share your thoughts and experiences in the comments below! Let's connect and grow together in the DevOps community. 😊

---