---
layout: post
title: "CI/CD Project Using AWS, Terraform, GitLab, Docker, Linux"
description: "Demonstration of application deployment using a CI/CD Pipeline"
tags: Projects
---

# CI/CD Project Using AWS, Terraform, GitLab, Docker, Linux

I chose this project to document the building of a CI/CD pipeline from start to end.

## Scenario
Launch a Django application that is scalable, secure, with zero downtime.

## Diagram
<img src="/images/pipeline-project.PNG" alt="project-overview" width="500px"/>

## Tools Used

- **Terraform:** Tool used to define AWS services in one location as the Infrastructure as Code(IAC) which supports multiple platforms. 

- **GitLab:** Used to store the source code of the application, manages merge requests, bug tracking, and project management.

- **CI/CD Pipelines:** managed by GitLab which automates the entire delivery process.

- **Docker:** A containerization tool used to deploy code. 

- **Django Rest Framework:** Django was used to build sample apps to display the CI/CD in action.

- **Linux Ubuntu:** Operating system.

## AWS Services
- **IAM:** (Identity and Access Management) controls access to the AWS account for both users and AWS computer based users. Policies were used to limit user access to absolute minimum as needed.

- **AWS ECS:** (Elastic Container Service)
A highly scalable and fast container management service used to manage your own servers or let ECS manage Docker for you. 

- **Fargate:** This is the serverless option. AWS manages the EC2 instance for you. This reduces the maintenance overhead and gives you the flexibility to integrate with other services.

- **EC2:** Virtual server on AWS.

- **DynamoDB:** NonSQL database used in conjunction with Terraform tfstate file. This helps to create a single point of entry to reduce access to the infrastructure and keeps account secure.

- **VPC:** (Virtual Private Cloud) used to keep resources separate and reduce the risk of breaking the whole infrastructure when making changes. Keeping the resources separate also improves security so if one environment is attacked the other environment is secure.

- **RDS:** (Relational Database Service) used to create databases for application. This is the managed solution which reduces maintenance overhead and makes it easier to scale up

- **Application Load Balancer:** is used to create zero downtime deployments. This service accepts and forwards tasks running in ECS. It waits for new updates before turning off old versions.

- **S3:** (Simple Storage Service) used to add persistent storage to the application. 

- **CloudWatch:** This service stores all the logs of the application in a central location. This makes debugging easier.

- **AWS Certificate Manager:**
Used to manage and create certificates for secure https access. 

I'll document process as I go.

