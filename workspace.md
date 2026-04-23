# 📘 Terraform Workspaces – Dev & Prod Environment Setup

## 🔹 Overview

Terraform **workspaces** allow you to manage **multiple environments (dev, prod, staging)** using the same configuration.

* Each workspace maintains its **own state file**
* Helps avoid duplication of code
* Enables environment-based deployments

---

## ⚙️ Step 1: Check Existing Workspaces

```bash
terraform workspace list
```

👉 Default workspace:

```
* default
```

---

## 🚀 Step 2: Create & Use DEV Environment

### Create Dev Workspace

```bash
terraform workspace new dev
```

### Switch to Dev

```bash
terraform workspace select dev
```

---

## 📦 Dev Configuration

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "6.41.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "webserver" {
  ami           = "ami-098e39bafa7e7303d"
  instance_type = "t3.large"
  count         = 1

  tags = {
    Name = "dev-server"
  }
}
```

---

## ▶️ Deploy Dev Infrastructure

```bash
terraform init
terraform plan
terraform apply
```

---

## 🔍 Verify Workspaces

```bash
terraform workspace list
```

Example:

```
default
* dev
```

---

## 🚀 Step 3: Create & Use PROD Environment

### Create Prod Workspace

```bash
terraform workspace new prod
```

### Switch to Prod

```bash
terraform workspace select prod
```

---

## 📦 Prod Configuration

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "6.41.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "webserver" {
  ami           = "ami-098e39bafa7e7303d"
  instance_type = "t3.large"
  count         = 1

  tags = {
    Name = "prod-server"
  }
}

resource "aws_eip" "webserver_ip" {
  domain = "vpc"
}

resource "aws_eip_association" "webserver_ip_assoc" {
  instance_id   = aws_instance.webserver[0].id
  allocation_id = aws_eip.webserver_ip.id
}
```

---

## ▶️ Deploy Prod Infrastructure

```bash
terraform init
terraform plan
terraform apply
```

---

# 🧠 Key Concepts

### ✅ Workspace Isolation

* Each workspace has separate:

  * State file
  * Resource tracking
* Example:

  * `dev` → dev EC2 instance
  * `prod` → prod EC2 + Elastic IP

---

### ✅ Same Code, Different Environments

Instead of duplicating files:

* Use **workspace-specific variables or logic**

---

### ✅ Current Workspace Check

```bash
terraform workspace show
```

---

### ✅ Delete Workspace

```bash
terraform workspace delete dev
```

⚠️ Cannot delete active workspace

---

# ⚠️ Best Practices

### 🔹 Use Workspace-Based Naming

```hcl
tags = {
  Name = "${terraform.workspace}-server"
}
```

---

### 🔹 Avoid Hardcoding Differences

Use variables:

```hcl
variable "instance_type" {}

instance_type = var.instance_type
```

---

### 🔹 Use Remote Backend (Recommended)

For real projects:

* S3 + DynamoDB (AWS)
* Azure Storage
* Terraform Cloud

---

### 🔹 Separate State for Safety

Never mix dev & prod state

---

# 🎯 Interview Questions

### 1. What is Terraform Workspace?

👉 Logical separation of state files for multiple environments

---

### 2. Default Workspace Name?

👉 `default`

---

### 3. Can Workspaces Share State?

👉 ❌ No, each has separate state

---

### 4. Use Case of Workspaces?

👉 Manage dev, staging, prod using same code

---

### 5. Limitation?

👉 Not ideal for:

* Completely different infrastructure
* Large-scale environment differences

---

# 📌 Summary Flow

```bash
terraform workspace new dev
terraform workspace select dev
terraform apply

terraform workspace new prod
terraform workspace select prod
terraform apply
```

---
