<!-- BEGIN_TF_DOCS -->

# **Terraform Module - ECS (Fargate)**

## **__Overview__**

This Terraform code provides an infrastructure deployment and automates the provisioning of resources as per folder structure.


## **Folder Structure**

This is the folder structure for the project:

- **config**
  ├── dev
  ├── test
  └── prod
- **infra**
  ├── s3
  ├── networking
  ├── loadbalancer
  └── ecs
- **modules**
  ├── vpc
  ├── subnet
  ├── route-table
  ├── nacl
  ├── s3
  ├── alb
  ├── sg
  ├── ecs-cluster-service
  ├── task-definition-fargate
  ├── app-autoscaling-target-fargate
  ├── iam-role-fargate
  └── ecr



## **Providers**

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [Terraform](#provider\_aws) | => 4 |


## **Modules**
1.[s3](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/s3) <br>
2.[vpc](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/vpc) <br>
3.[subnet](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/subnet) <br>
4.[route-table](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/route-table) <br>
5.[nacl](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/nacl) <br>
6.[alb](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/alb) <br>
7.[sg](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/sg) <br>
8.[ecs-cluster-service-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/ecs-cluster-service-fargate) <br>
9.[task-defination-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/task-defination-fargate) <br>
10.[app-autoscaling-target-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/app-autoscaling-target-fargate) <br>
11.[iam-role-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/iam-role-fargate) <br>
12.[ecr](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/tree/main/modules/ecr) <br>


## **Resources**
| Name | Type | Infra |
|------|------|-------|
| [s3](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/s3/main.tf) | resource | s3 |
| [vpc](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/vpc/main.tf) | resource | networking |
| [subnet](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/subnet/main.tf) | resource | networking |
| [route-table](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/route-table/main.tf) | resource | networking |
| [nacl](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/nacl/main.tf) | resource | networking |
| [alb](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/alb/main.tf) | resource | loadbalancer |
| [sg](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/sg/main.tf) | resource | loadbalancer & ecs |
| [ecs-cluster-service-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/ecs-cluster-service-fargate/main.tf) | resource | ecs |
| [task-defination-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/task-defination-fargate/main.tf) | resource | ecs |
| [app-autoscaling-target-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/app-autoscaling-target-fargate/main.tf) | resource | ecs |
| [iam-role-fargate](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/iam-role-fargate/main.tf) | resource | ecs |
| [ecr](https://github.com/technocirrus-devops/AWS-Infrastructure-using-Terraform/blob/main/modules/ecr/main.tf) | resource | ecs |


## **Infra**

**S3:**
| Name | Description |
|------|-------------|
| `s3.tf` |This file defines a Terraform module named "s3" that creates an S3 bucket. It specifies various configuration parameters such as the bucket name, access control, versioning, encryption, lifecycle rules, and more. It includes the module source, dependencies, and references the policy.json file for bucket policies. |
| `policy.json` | This file contains the IAM policy document in JSON format. It defines the permissions for the S3 bucket. It allows the AWS Elastic Load Balancing service to write logs to a specific prefix within the bucket, grants access to a specific IAM user to upload objects to another prefix within the bucket, and sets access conditions based on the AWS account and ARN. The policy is used in the s3.tf file to apply the desired permissions to the bucket. |
| `variables.tf` | This file defines input variables for the S3 bucket module. It specifies the types and descriptions of each variable, such as the bucket name, force destroy flag, bucket tags, ACL, versioning status, encryption algorithm, access control settings, lifecycle rules, and more. |
| `outputs.tf` | This file defines the outputs of the S3 bucket module. It specifies the bucket ID and ARN as the output values, which can be used by other Terraform modules or scripts. |
| `provider.tf` |  This file specifies the AWS provider configuration, setting the region based on the provider_region variable. |


**Networking:**
| Name | Description |
|------|-------------|
| `vpc.tf` | This file defines the main VPC module and configures various parameters such as VPC CIDR block, instance tenancy, DNS support, VPC tags, etc. It also specifies the source module location and sets up VPC flow logs. |
| `subnet.tf` | This file includes the subnet module, which creates public and private subnets within the VPC. It references the VPC module's outputs and defines parameters like subnet CIDRs, availability zones, and association with route tables. |
| `route-table.tf` | This file contains the route table module, which sets up public and private route tables for the subnets. It associates the public route table with the internet gateway and the private route table with a NAT gateway. |
| `nacl.tf` | This file uses the NACL module to create network access control lists (NACLs) for both the public and private subnets. It configures ingress and egress rules for the NACLs. |
| `data.tf` | This file retrieves information about an AWS S3 bucket using the aws_s3_bucket data source. |
| `variables.tf` | This file declares input variables used in the VPC module, such as provider region, VPC CIDR block, instance tenancy, DNS configurations, VPC tags, subnet details, route table details, NACL rules, and more. |
| `outputs.tf` | This file defines the outputs of the VPC infrastructure, such as VPC ID, internet gateway ID, subnet IDs, NAT gateway ID, route table IDs, and DHCP options. |
| `provider.tf` |   This file specifies the AWS provider configuration, setting the region based on the provider_region variable. |



**Loadbalancer:**
| Name | Description |
|------|-------------|
| `alb.tf` |This file sets up an Application Load Balancer (ALB) using the alb module source. It includes input variables like alb_name, internal, alb_sg, alb_subnets, ip_address_type, load_balancer_type, alb_tag, bucket_name, alb_prefix, alb_target, vpc_id, alb_listener, and alb_listener_rule to configure the ALB. |
| `alb-sg.tf` | This file defines a security group (SG) module using the sg module source. It takes input variables such as sg_name, sg_tag, vpc_id, ingress, source_security_group_id, and egress to create the security group. |
| `data.tf` | This file retrieves information about the VPC, subnets, and an S3 bucket using the aws_vpc, aws_subnet, and aws_s3_bucket data sources, respectively. It fetches data based on input variables such as vpc_tags, data_public_subnet_1_name, data_public_subnet_2_name, and bucket_name. |
| `variables.tf` | This file declares all the input variables used in the configuration. It includes variables for the provider region, VPC tags, public subnet names, ALB configuration, ALB listener configuration, ALB listener rule configuration, security group configuration, ALB prefix, and bucket name. |
| `outputs.tf` | This file defines outputs for the ALB and security group. It exposes values such as alb_arn, alb_arn_suffix, alb-dns-name, target_arn, and sg_id to retrieve information about the created ALB and security group. |
| `provider.tf` |  This file specifies the AWS provider configuration, setting the region based on the provider_region variable. |


**ECS:**
| Name | Description |
|------|-------------|
| `ecs-cluster-service.tf` | This file defines the ECS Fargate cluster and service using the ecs-cluster-service-fargate module. It includes parameters like cluster name, container name, container port, ECS service name, target group ARN, security group ID, and subnets. |
| `ecs-task-definition.tf` | This file defines the ECS Fargate task definition using the task-defination-fargate module. It includes parameters like family name, memory, CPU, network mode, compatibility, execution role ARN, and container definitions from a JSON file. |
| `app-autoscaling.tf` | This file configures application autoscaling for the ECS Fargate service using the app-autoscaling-target-fargate module. It includes parameters like maximum capacity, minimum capacity, cooldown period, cluster name, and service name. |
| `ecs-sg.tf` | This file sets up the security group for the ECS Fargate cluster using the sg module. It includes parameters like security group name, tags, VPC ID, ingress rules, egress rules, and references the ALB security group. |
| `ecs-iam-role.tf` | This file creates an IAM role for ECS Fargate using the iam-role-fargate module. It includes parameters like ECS role name. |
| `ecr.tf` | This file creates an ECR repository using the ecr module. It includes parameters like repository name, image tag mutability, and scan on push settings. |
| `data.tf` | This file contains data sources to fetch information like VPC, subnets, ALB target group ARN, and ALB security group. |
| `outputs.tf` | This file defines the outputs of the Terraform deployment, including role ARN, cluster name, cluster ID, ECS service name, task definition ARN, ECR repository URL, and security group ID. |
| `variables.tf` | This file defines the outputs of the Terraform deployment, including role ARN, cluster name, cluster ID, ECS service name, task definition ARN, ECR repository URL, and security group ID. |
| `outputs.tf` | This file declares all the variables used in the Terraform configurations, including VPC tags, subnet names, ALB target group, security group tags, ingress/egress rules, ECS cluster/service parameters, autoscaling settings, ECS role name, and ECR repository settings. |
| `provider.tf` |  This file specifies the AWS provider configuration, setting the region based on the provider_region variable. |




## **Deployment Order**

When deploying the infrastructure using this Terraform configuration, it is important to follow the correct order of resource creation to ensure proper dependencies and functionality. Here's the recommended deployment order:

1. Create the S3 Bucket: The S3 bucket is required for storing VPC flow logs. Create the bucket first as other resources depend on it.

2. Create the VPC and Its Resources: Proceed with creating the VPC and its associated resources, including subnets, route tables, security groups, and network ACLs. These resources form the foundation of your network infrastructure.

3. Create the Application Load Balancer (ALB): Once the VPC and its resources are in place, create the ALB. The ALB serves as the entry point for incoming traffic and routes it to the appropriate ECS services.

4. Create the ECS Services: Finally, create the ECS services that will host your applications. These services will be registered with the ALB and configured to handle incoming requests.



<!-- END_TF_DOCS -->
