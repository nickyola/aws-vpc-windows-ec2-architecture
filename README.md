Hands-on AWS networking project demonstrating VPC creation, subnet segmentation, internet connectivity, security group configuration, and Windows VM deployment.
![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws)
![Amazon EC2](https://img.shields.io/badge/Amazon-EC2-yellow?logo=amazonaws)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue?logo=amazonaws)
![Windows Server](https://img.shields.io/badge/OS-Windows%20Server-0078D6?logo=windows)
![Cloud Architecture](https://img.shields.io/badge/Architecture-Network%20Design-green)
![Infrastructure](https://img.shields.io/badge/Infrastructure-IaC%20Ready-purple)
![Free Tier](https://img.shields.io/badge/AWS-Free%20Tier-success)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

##  Table of Contents

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

---
# AWS VPC Architecture and Windows EC2 Deployment

##  Project Overview

This project demonstrates how I designed and deployed a complete AWS networking environment by creating a Virtual Private Cloud (VPC) and successfully launching a Windows EC2 instance.

Before deploying any infrastructure, I created an architectural diagram using Draw.io.  
This diagram served as a blueprint for the entire environment and helped me visualize the network structure before implementation.

Designing the architecture beforehand made the deployment smoother and reduced configuration errors.”

---
## 🏗️ AWS Architecture Diagram

![Architecture](Images/AWS%20Architecture%20Diagram.PNG)

The diagram illustrates:

- A custom VPC
- Three public subnets
- Internet Gateway for internet connectivity
- Route table configuration
- Security Group for access control
- Windows EC2 instance deployed in the Front-end subnet

---

## ⚙️ Planning and Preparing the Environment

The first step was creating a **VPC**, since all AWS resources such as EC2 instances, subnets, route tables, and gateways must exist inside a VPC.

For this test environment, I created **three public subnets** to allow easy internet access.

In a production environment, a more secure design would include:

- Two public subnets
- Two private subnets

However, for testing and learning purposes, three public subnets were sufficient.

---

## 🌐 Creating the VPC

A **Virtual Private Cloud (VPC)** is a logically isolated network in AWS where cloud resources can be launched securely.

### Steps:

1. Navigated to the AWS Management Console.
2. Searched for VPC in the AWS search bar and opened the VPC Dashboard.

![VPC Dashboard](Images/VPC%20Dashboard%20.PNG)

3. Clicked **Create VPC**
4. Configured the VPC:

- Name: `accessbank-vm`
- IPv4: Enabled
- IPv6: Disabled
- Auto-assign public IPv4: Enabled
- Tenancy: Default

5. Clicked **Create VPC**.

The VPC was successfully created and appeared in the dashboard.

![Create VPC](Images/Creating%20Custom%20VPC.PNG)


## 🧩 Creating Subnets

Subnets were created to logically organize resources within the VPC.

### Subnets Created:

- **Front-end-subnet** → For public-facing applications and EC2 instances
- **Backend-subnet** → For internal application services
- **Database-subnet** → For secure database deployment
  
![Frontend Subnet](Images/Frontend%20Subnet%20Configuration.PNG)

![Backend Subnet](Images/Backend%20Subnet%20Configuration.PNG)

![Database Subnet](Images/Database%20Subnet%20Configuration.PNG)
  

This structure improves:

- Security
- Traffic routing
- Resource organization
- Scalability

---

## 🌍 Configuring Internet Connectivity

To allow remote access to the Windows VM, internet connectivity was required.

### Steps:

1. Created an **Internet Gateway (IGW)**.

![Internet Gateway](Images/Internet%20Gateway%20Setup.PNG)

2. Attached the IGW to the VPC.
3. Created a **Route Table**.
4. Associated the Route Table with the **Front-end subnet**.

![Route Table](Images/Route%20Table%20Configuration.PNG)

5. Associated the **Front-end subnet** with a Network ACL for additional traffic control.

![Network ACL](Images/Network%20ACL%20Configuration.PNG)

6. Added the following route:

 0.0.0.0/0 → Internet Gateway
7. Verified that the Front-end subnet was configured to **auto-assign public IP addresses**.

This enabled external connectivity to the EC2 instance.


## 🔐 Security Group Configuration

Before launching the EC2 instance, a **Security Group** was created to control inbound and outbound traffic.

![Security Group](Images/Security%20Group%20Configuration.PNG)

### Rules Configured:

- Allowed **RDP access (TCP Port 3389)** only from my personal IP address.
- Allowed default outbound traffic so the instance could access the internet for updates.

This ensured secure remote access to the Windows server.

---

## 💻 Launching the Windows EC2 Instance
### Launch EC2 Instance Page

After completing the network setup, I proceeded to launch the EC2 instance.

 ![Launch EC2](Images/Launch%20EC2%20Instance%20Page.PNG)
 
### Configuration Details:

- **Operating System:** Windows Server
  
![Windows AMI](Images/Windows%20AMI%20Selection.PNG)
  
- **Instance Type:** t3.micro (Free-tier eligible and suitable for testing)

![Instance Type](Images/Instance%20Type%20Selection.PNG)
  
- **Subnet:** Front-end subnet
- **Auto-assign Public IP:** Enabled
- **Security Group:** Attached the previously created RDP Security Group
- **Storage:** Default General Purpose SSD (gp2)
- **Key Pair:** Created a new key pair for secure login

The key pair is required to **decrypt the Administrator password** when connecting via Remote Desktop.

After reviewing all settings, I clicked **Review Launch**

![Review Launch](Images/Instance%20Review%20and%20Launch.PNG)

**Launch Instance**.

Within a few minutes, the Windows virtual machine was successfully deployed.

![Launch Success](Images/EC2%20Launch%20Success%20Message.PNG)

---

## 🖥️ Connecting to the Windows VM via RDP

Once the instance was running:

1. Copied the **Public IP Address** from the EC2 dashboard.
2. Opened **Remote Desktop Connection (RDP)** on my local computer.
   
 ![RDP Client](Images/Remote%20Desktop%20Client%20Connection.PNG)
   
3. Entered the Public IP.
4. Used the **Administrator username**.
5. Decrypted the password using the downloaded key pair.

   ![Get Password](Images/Retrieve%20Windows%20Administrator%20Password.PNG)

After connecting, the screen switched seamlessly to the remote Windows desktop environment.

![Windows Desktop](Images/Successful%20RDP%20Connection%20to%20Windows%20Server.PNG)

This allowed me to work on the virtual machine remotely from anywhere, just like using a physical computer.

---

## ✅ Conclusion

This project demonstrates practical knowledge of:

- AWS VPC Design
- Subnet Architecture
- Internet Gateway Configuration
- Route Table Management
- Security Group Implementation
- Windows EC2 Deployment
- Remote Desktop Connectivity

Designing the architecture before deployment improved efficiency and reduced configuration errors.

This hands-on implementation strengthened my understanding of AWS networking fundamentals and cloud infrastructure deployment.

---

## 🚀 Future Improvements

- Implement private subnets for backend and database layers
- Deploy NAT Gateway for secure outbound internet access
- Introduce Load Balancer for high availability
- Apply Infrastructure as Code using Terraform or CloudFormation
- Enable monitoring with CloudWatch

  
