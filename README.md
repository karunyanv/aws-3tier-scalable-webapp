# 🚀 Scalable 3-Tier Web Application on AWS (Free Tier)

## 📌 Overview

This project demonstrates the design and deployment of a **highly available and scalable 3-tier architecture** on AWS using free-tier eligible services.

The architecture follows industry best practices:

* Separation of concerns (presentation, application, data)
* High availability across multiple Availability Zones
* Auto scaling for performance and cost optimization
* Secure networking using public and private subnets

---

## 🧩 Architecture

![Architecture Diagram](architecture.png)

---

## 🏗️ Architecture Components

### 1. Presentation Layer

* Application Load Balancer (ALB)
* Internet-facing
* Distributes incoming HTTP traffic

### 2. Application Layer

* EC2 instances (Amazon Linux)
* Auto Scaling Group (ASG)
* Hosts web application (Apache/PHP)

### 3. Data Layer

* Amazon RDS (MySQL)
* Hosted in private subnet
* Secure and not publicly accessible

---

## ⚙️ AWS Services Used

* Amazon EC2
* Application Load Balancer (ALB)
* Amazon RDS (MySQL)
* Auto Scaling Group
* Amazon VPC
* CloudWatch (basic monitoring)

---

## 🌐 Network Design

* Custom VPC (10.0.0.0/16)
* 2 Public Subnets (ALB)
* 2 Private Subnets (EC2 + RDS)
* Internet Gateway attached
* Route tables configured for isolation

---

## 🔧 Deployment Steps

### Step 1: Create VPC

* Configure CIDR block
* Create public & private subnets
* Attach Internet Gateway

### Step 2: Launch RDS (Database)

* MySQL (Free Tier)
* Private subnet only
* Security group allows EC2 access

### Step 3: Configure EC2 Instance

* Install Apache & PHP
* Connect to RDS database
* Create test application

Example:

```php
<?php
$conn = new mysqli("RDS-ENDPOINT", "admin", "password", "mydb");
echo "Connected successfully!";
?>
```

### Step 4: Create AMI

* Create image from configured EC2 instance

### Step 5: Configure ALB

* Internet-facing
* Target group linked to EC2 instances

### Step 6: Setup Auto Scaling Group

* Min: 1 | Desired: 2 | Max: 3
* Attach to ALB

### Step 7: Configure Scaling Policy

* Scale out: CPU > 60%
* Scale in: CPU < 30%

---

## 📈 Testing & Validation

* Load testing using Apache Benchmark:

```
ab -n 1000 -c 50 http://<ALB-DNS>
```

* Verified:

  * Traffic distribution
  * Auto scaling behavior
  * High availability

---

## 🔐 Security Best Practices

* RDS deployed in private subnet
* Security groups restrict access between layers
* No direct public access to EC2 instances
* Only ALB exposed to internet

---

## 💰 Cost Optimization (Free Tier)

* EC2: t2.micro / t3.micro
* RDS: db.t3.micro
* Total usage within 750 hours/month
* Resources terminated after testing

---

## 📊 Key Learnings

* Designing scalable cloud architecture
* Implementing Auto Scaling & Load Balancing
* VPC networking and subnet isolation
* Secure database deployment
* High availability design patterns

---

## 📌 Future Improvements

* CI/CD pipeline using GitHub Actions
* HTTPS with ACM & Route 53
* Docker containerization
* Infrastructure as Code (Terraform)

---

## 👨‍💻 Author

Karunyan V
AWS Certified Solutions Architect – Associate
