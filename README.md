# aws-vpc-windows-ec2-architecture
AWS VPC architecture project showcasing subnet design, internet connectivity setup, and Windows EC2 remote access configuration.

Hands-on AWS networking project demonstrating VPC creation, subnet segmentation, internet connectivity, security group configuration, and Windows VM deployment.

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws)
![Amazon EC2](https://img.shields.io/badge/Amazon-EC2-yellow?logo=amazonaws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazonaws)
![Windows Server](https://img.shields.io/badge/OS-Windows%20Server-0078D6?logo=windows)
![Cloud Architecture](https://img.shields.io/badge/Architecture-Network%20Design-green)
![Infrastructure](https://img.shields.io/badge/Infrastructure-IaC%20Ready-purple)
![Free Tier](https://img.shields.io/badge/AWS-Free%20Tier-success)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

## 📚 Table of Contents

- [Project Overview](#-project-overview)
- [Architecture Diagram](#️-aws-architecture-diagram)
- [Environment Planning](#️-planning-and-preparing-the-environment)
- [Creating the VPC](#-creating-the-vpc)
- [Creating Subnets](#-creating-subnets)
- [Configuring Internet Connectivity](#-configuring-internet-connectivity)
- [Security Group Configuration](#-security-group-configuration)
- [Launching the Windows EC2 Instance](#-launching-the-windows-ec2-instance)
- [Connecting via Remote Desktop](#️-connecting-to-the-windows-vm-via-rdp)
- [Conclusion](#-conclusion)
- [Future Improvements](#-future-improvements)
  
# AWS VPC Architecture and Windows EC2 Deployment

This project demonstrates how I designed and deployed a complete AWS networking environment by creating a Virtual Private Cloud (VPC) and successfully launching a Windows EC2 instance.

Before deploying any infrastructure, I created an architectural diagram using Draw.io.  
This diagram served as a blueprint for the entire environment and helped me visualize the network structure before implementation.

Designing the architecture beforehand made the deployment smoother and reduced configuration errors.

## AWS Architecture Diagram

![Architecture](Images/AWS%20Architecture%20Diagram.PNG)

## Planning and Preparing the Environment

The first step was creating a VPC, since all AWS resources such as EC2 instances, subnets, route tables, and gateways must exist inside a VPC.

For this test environment, I created three public subnets to allow easy internet access.

In a production environment, a more secure design would include:

- Two public subnets  
- Two private subnets  

However, for testing and learning purposes, three public subnets were sufficient.

## Creating the VPC

A Virtual Private Cloud (VPC) is a logically isolated network in AWS where cloud resources can be launched securely.

1. Navigated to AWS Management Console  
2. Searched for VPC and opened the dashboard  

![VPC Dashboard](Images/VPC%20Dashboard%20.PNG)

Configured:

- Name: accessbank-vm  
- IPv4 enabled  
- IPv6 disabled  
- Auto-assign public IPv4 enabled  
- Tenancy default  

![Create VPC](Images/Creating%20Custom%20VPC.PNG)

## Creating Subnets

- Front-end-subnet  
- Backend-subnet  
- Database-subnet  

![Frontend Subnet](Images/Frontend%20Subnet%20Configuration.PNG)

![Backend Subnet](Images/Backend%20Subnet%20Configuration.PNG)

![Database Subnet](Images/Database%20Subnet%20Configuration.PNG)

## Configuring Internet Connectivity

![Internet Gateway](Images/Internet%20Gateway%20Setup.PNG)

![Route Table](Images/Route%20Table%20Configuration.PNG)

![Network ACL](Images/Network%20ACL%20Configuration.PNG)

Route added:

0.0.0.0/0 → Internet Gateway
