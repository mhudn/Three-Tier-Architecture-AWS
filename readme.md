# AWS Three-Tier Architecture with Terraform

This repository contains Terraform code to deploy a Three-Tier Architecture on AWS. The architecture consists of three tiers: Web, Application, and Database, each residing in separate subnets within a Virtual Private Cloud (VPC).

## Prerequisites

Before deploying the Three-Tier Architecture, ensure you have the following prerequisites:

- [Terraform](https://www.terraform.io/) installed on your local machine.
- Appropriate AWS credentials configured to allow Terraform to create resources on your behalf.

## Architecture Overview

The Three-Tier Architecture consists of the following components:

1. **VPC:** A Virtual Private Cloud that serves as the networking foundation for the architecture.

2. **Web Tier:** A group of EC2 instances running web servers to handle incoming user requests.

3. **Application Tier:** A group of EC2 instances running the application logic that processes user requests.

4. **Database Tier:** An RDS (Relational Database Service) instance to store and manage the application's data.

## Terraform Variables

To customize the deployment of the Three-Tier Architecture, the following Terraform variables are available in the `variables.tf` file:

### Count Variable

- `item_count`: The number of instances to deploy in each tier. Default value is 2.

### VPC Variables

- `vpc_cidr`: The CIDR block for the VPC. Default value is "10.0.0.0/16".
- `availability_zone_names`: A list of availability zone names where the subnets will be created. Default value is ["us-east-1a", "us-east-1b"].
- `web_subnet_cidr`: A list of CIDR blocks for the web tier subnets. Default value is ["10.0.1.0/24", "10.0.2.0/24"].
- `application_subnet_cidr`: A list of CIDR blocks for the application tier subnets. Default value is ["10.0.11.0/24", "10.0.12.0/24"].
- `database_subnet_cidr`: A list of CIDR blocks for the database tier subnets. Default value is ["10.0.21.0/24", "10.0.22.0/24"].

### Instance Variables

- `ami_id`: The ID of the Amazon Machine Image (AMI) to be used for EC2 instances. Default value is "ami-0d5eff06f840b45e9".
- `instance_type`: The instance type for EC2 instances. Default value is "t2.micro".

### Database Variables

- `rds_instance`: A map of configuration settings for the RDS instance. Default values are provided for the following keys:
  - `allocated_storage`: The allocated storage for the database (in GB). Default value is 10.
  - `engine`: The database engine to use (e.g., "mysql").
  - `engine_version`: The version of the database engine.
  - `instance_class`: The instance class for the RDS instance.
  - `multi_az`: Set to `false` to disable multi-AZ deployment.
  - `name`: The name of the RDS instance.
  - `skip_final_snapshot`: Set to `true` to skip the final database snapshot during termination.

### Database Sensitive Variables

- `user_information`: A map containing sensitive information for the database user. Default values are provided for the following keys:
  - `username`: The username for the database user.
  - `password`: The password for the database user. This is marked as sensitive and will not be displayed in Terraform output.

## Deployment Instructions

1. Clone this repository to your local machine.

2. Navigate to the repository's root directory.

3. Modify the `variables.tf` file to set the desired values for the Terraform variables, if needed.

4. Initialize Terraform by running the following command:

   ```
   terraform init
   ```

5. View the execution plan to see what resources will be created:

   ```
   terraform plan
   ```

6. If the execution plan looks good, apply the changes to create the infrastructure:

   ```
   terraform apply
   ```

7. Terraform will prompt for confirmation before proceeding. Enter `yes` to proceed with the deployment.

8. After the deployment is complete, Terraform will output the public IP addresses or DNS names of the web instances, which can be used to access the application.

## Clean Up

To clean up and destroy all the resources created by Terraform, run the following command:

```
terraform destroy
```

Terraform will prompt for confirmation before proceeding. Enter `yes` to destroy the infrastructure.

## Disclaimer

Ensure that you have the necessary AWS credentials set up correctly on your local machine before running Terraform.

Please be aware that this Terraform code will create AWS resources, which may incur costs. Ensure that you review the resources created and their associated costs before deploying this architecture.

Make sure to review the Terraform code and modify the variables according to your specific requirements before applying the changes.

Be cautious with sensitive data, such as passwords and access keys. Always use secure methods to manage and handle sensitive information.
This Terraform code is intended for educational and demonstration purposes. In production environments, consider adding security measures, monitoring, and other best practices.