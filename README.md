# 📘 Hosting a Static Website on AWS — Basic Architecture Overview

This README provides a clear overview of the **services used**, the **architecture**, and the **project flow** for hosting a static website on AWS.

👉 **For detailed step-by-step instructions and implementation steps, please refer to the full Project Guide.**

---

## 🛠️ Services Used

### **Networking & Connectivity**

* **VPC (Virtual Private Cloud)** – Custom private network for the entire architecture
* **Subnets** – Public and private subnets across two Availability Zones
* **Internet Gateway** – Enables internet access for public subnets
* **NAT Gateway** – Allows private instances to access the internet securely
* **Route Tables** – Controls traffic routing in public and private networks

### **Compute & Scaling**

* **EC2 (Elastic Compute Cloud)** – Web servers (private) and Bastion host (public)
* **Launch Template** – Blueprint for EC2 configurations
* **Auto Scaling Group** – Automatically adds/removes EC2 instances based on demand

### **Storage**

* **S3 Bucket** – Stores static website content or deployment files

### **Security & Identity**

* **IAM Role** – EC2 access to S3
* **Security Groups** – Controls inbound/outbound traffic for ALB, EC2, Bastion

### **Load Balancing & Routing**

* **Application Load Balancer (ALB)** – Distributes traffic across EC2 instances
* **Target Group** – Registers and health-checks web EC2 instances
* **Route 53** – Domain management & DNS routing
* **Certificate Manager (ACM)** – SSL/TLS certificates for HTTPS

---

## 🏗️ Basic Architecture

The project follows a **highly available 2-tier architecture** spread across two AWS Availability Zones.

### **1️⃣ Networking Layer**

* A VPC is created with **public** and **private** subnets in **AZ1** and **AZ2**.
* Public subnets host:

  * Bastion host
  * NAT Gateway
  * Application Load Balancer
* Private subnets host:

  * EC2 Web servers (attached to Target Group)
  * App and Data tier separation using dedicated subnets

### **2️⃣ Security Layer**

* Bastion host allows secure SSH into private EC2 servers
* Only ALB is exposed to the public internet
* Private EC2 servers only accept traffic from ALB

### **3️⃣ Compute Layer**

* Web EC2 instances reside in private subnets
* Connected to S3 via IAM roles (for deployment or file access)
* Auto Scaling Group ensures high availability

### **4️⃣ Load Balancing Layer**

* Application Load Balancer receives all incoming requests
* Distributes requests across healthy EC2 instances
* ALB uses HTTPS (SSL from ACM) and redirects HTTP → HTTPS

### **5️⃣ Domain & SSL Layer**

* Route 53 maps domain (e.g., `www.example.com`) to ALB
* Certificate Manager issues SSL for secure browsing

---

## 🔄 Basic Project Flow (Request Lifecycle)

```
User → Browser → Route53 DNS → ALB (HTTPS) → Target Group → Private EC2 → S3 (if needed)
```

### **Detailed Flow:**

1. User enters the domain (e.g., `www.example.com`)
2. Route53 resolves the domain to the ALB DNS
3. ALB receives the request (HTTPS)
4. ALB forwards the request to the target group
5. Auto Scaling Group ensures sufficient EC2 instances are running
6. Private EC2 instance processes request and serves content (or fetches from S3)
7. Response is sent securely back to the user

---

## 📄 Full Project Guide

For detailed instructions such as:

* Creating VPC, subnets, route tables
* Launching EC2 instances
* Configuring ALB, Target Groups, Auto Scaling
* Applying IAM roles & SG rules
* Uploading files to S3
* Setting up Route53 and SSL

👉 **Please refer to the complete Project Guide document.** [Project Guide](https://docs.google.com/document/d/1sm0pwNgMkBJzfVzad_azJdk0wFdVOvz1F3kcmiVLbeE/edit?usp=sharing)

---
