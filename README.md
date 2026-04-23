# 🚀 Terraform Complete Study 
---

# 🟢 PHASE 1: Fundamentals (Day 1)

## 🔹 Understand Basics

* What is Terraform (IaC – Declarative)
* Why Terraform vs manual provisioning
* Multi-cloud support via HashiCorp

---

## 🔹 Install & Verify

```bash
terraform -version
```

---

## 🔹 First Commands

```bash
terraform init
terraform validate
terraform fmt
terraform plan
terraform apply
terraform destroy
```

---

## 🔹 Points to Remember

* Always run `init` first
* Never skip `plan`
* Terraform is **idempotent**

---

# 🟡 PHASE 2: Core Concepts (Day 2)

## 🔹 Basic Structure

```hcl
provider "aws" {}

resource "aws_instance" "web" {
  ami           = "ami-xyz"
  instance_type = "t2.micro"
}
```

---

## 🔹 Key Concepts

* Provider → Cloud connection
* Resource → Infra component
* Variables → Dynamic values
* Output → Return values

---

## 🔹 Commands Practice

```bash
terraform plan -out=tfplan
terraform apply tfplan
terraform output
```

---

## 🔹 Points to Remember

* Do NOT hardcode values
* Use variables + outputs
* Keep code clean (`fmt`)

---

# 🟠 PHASE 3: State & Backend (Day 3)

## 🔹 Terraform State

* File: `terraform.tfstate`
* Maps config ↔ real infra

---

## 🔹 State Commands

```bash
terraform state list
terraform state show <resource>
terraform state rm <resource>
terraform state mv old new
```

---

## 🔹 Remote Backend (IMPORTANT)

```hcl
terraform {
  backend "s3" {
    bucket = "tf-state"
    key    = "dev/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

---

## 🔹 Points to Remember

* Never delete state file
* Use remote backend + locking
* Avoid multiple users on local state

---

# 🔵 PHASE 4: Variables + Environments (Day 4)

## 🔹 Variables

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

---

## 🔹 tfvars Usage

```bash
terraform apply -var-file=dev.tfvars
```

---

## 🔹 Workspaces

```bash
terraform workspace new dev
terraform workspace select dev
```

---

## 🔹 Points to Remember

* Use `.tfvars` for environments
* Workspace is **not full isolation**
* Prefer separate backend for prod

---

# 🟣 PHASE 5: Modules (Day 5) ⭐ MOST IMPORTANT

## 🔹 Concept

👉 Reusable Terraform components

---

## 🔹 Structure

```bash
modules/
 ├── ec2/
 ├── vpc/
```

---

## 🔹 Example

```hcl
module "ec2" {
  source         = "./modules/ec2"
  instance_type  = "t2.micro"
}
```

---

## 🔹 Types

* Local modules
* GitHub modules
* Terraform Registry modules

---

## 🔹 Points to Remember

* One module = one responsibility
* Always use variables + outputs
* Version your modules

---

# 🔴 PHASE 6: Advanced Commands (Day 6)

## 🔹 Debugging

```bash
export TF_LOG=DEBUG
```

---

## 🔹 Target Resource

```bash
terraform apply -target=aws_instance.web
```

---

## 🔹 Replace Resource

```bash
terraform apply -replace=aws_instance.web
```

---

## 🔹 Import Existing Infra

```bash
terraform import aws_instance.web i-123456
```

---

## 🔹 Graph Dependencies

```bash
terraform graph | dot -Tpng > graph.png
```

---

## 🔹 Points to Remember

* Avoid `-target` in production
* Use import for existing infra
* Understand dependencies

---

# ⚫ PHASE 7: Real DevOps Usage (Day 7)

## 🔹 CI/CD Integration

* Jenkins / GitHub Actions
* Automated provisioning

---

## 🔹 Best Practices

* Git version control
* Remote backend
* Modular design
* Separate environments

---

## 🔹 Security

* Use Secrets Manager / Key Vault
* Avoid hardcoded credentials

---

# 🎯 PHASE 8: Interview Preparation

---

## 🔹 Basic Questions

### What is Terraform?

👉 IaC tool to provision infra declaratively

---

### What is State?

👉 Mapping of infra + config

---

### Plan vs Apply?

👉 Preview vs execution

---

## 🔹 Intermediate Questions

### What is Backend?

👉 Remote state storage

---

### count vs for_each?

👉 Index vs key-based iteration

---

### Modules?

👉 Reusable infra blocks

---

## 🔹 Advanced Questions

### How do you manage state in teams?

👉 Remote backend + locking + RBAC

---

### How do you secure secrets?

👉 Vault / Secrets Manager

---

### What if state file is lost?

👉 Restore backup / infra drift issue

---

# 🔥 Scenario-Based Questions

---

## 🔹 Scenario 1: Multi-environment setup

👉 Modules + tfvars + separate backend

---

## 🔹 Scenario 2: Zero downtime deployment

👉 lifecycle:

```hcl
create_before_destroy = true
```

---

## 🔹 Scenario 3: Existing infra

👉 Use `terraform import`

---

## 🔹 Scenario 4: Team conflict

👉 Remote backend + locking

---

# 🧪 FINAL PRACTICE ROADMAP (IMPORTANT)

---

## ✅ Task 1 (Beginner)

* Create EC2 instance

---

## ✅ Task 2 (Intermediate)

* VPC + Subnet + EC2

---

## ✅ Task 3 (Advanced)

* ALB + Auto Scaling + EC2

---

## ✅ Task 4 (Pro Level)

* Modules (VPC + EC2 + RDS)

---

## ✅ Task 5 (Enterprise)

* Remote backend + CI/CD pipeline

---

# 💡 Architect-Level Final Points (Must Say)

👉

* “We use Terraform with **modular architecture**”
* “State is stored in **remote backend with locking**”
* “We follow **GitOps + CI/CD automation**”
* “We design infra for **scalability & reusability**”

---
