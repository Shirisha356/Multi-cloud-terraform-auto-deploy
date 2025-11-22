# Multi-cloud-terraform-auto-deploy
Multi-cloud Terraform project that auto-deploys Nginx web servers on AWS EC2 and GCP Compute Engine, with a shell-based health check.

multi-cloud-terraform-auto-deploy/

├── README.md
├── main.tf
├── variables.tf
├── terraform.tfvars
├── health_check.sh
├── aws/
│   └── ec2.tf
└── gcp/
    └── compute.tf

# Multi-Cloud Auto Deployment using Terraform

This project uses **Terraform** to deploy a simple Nginx-based web server in **two clouds**:

- **AWS EC2 instance**
- **GCP Compute Engine instance**

Both servers serve a basic HTML page:
- AWS page shows: `AWS Server Running`
- GCP page shows: `GCP Server Running`

A simple **health check script** (`health_check.sh`) then verifies both servers are reachable and responding correctly.

---

## 1. What You’ll Learn

- How to use **Terraform** with multiple providers (AWS + GCP)
- How to deploy:
  - An EC2 instance on AWS
  - A Compute Engine instance on GCP
- How to run a simple **health check** on both servers
- How to **destroy** (clean up) all resources with one command

---

## 2. Prerequisites

You should have:

1. **Operating System**
   - Linux VM / WSL / Cloud Shell / any Linux-like terminal (Ubuntu is fine)

2. **Accounts**
   - AWS account (Free Tier is fine)
   - GCP account (Free Tier / free trial is fine)

3. **Installed Tools**
   - [x] Terraform
   - [x] AWS CLI
   - [x] gcloud CLI (Google Cloud SDK)
   - [x] Git (for cloning/pushing to GitHub)

---

## 3. Project Architecture

High-level idea:

- **AWS:**
  - 1 EC2 instance (Ubuntu, `t2.micro`)
  - Security group allowing HTTP (`80`) from anywhere
  - User data installs Nginx and serves a simple HTML page

- **GCP:**
  - 1 Compute Engine instance (Ubuntu)
  - Firewall rule allowing HTTP (`80`) from anywhere
  - Startup script installs Nginx and serves a simple HTML page

- **Health Check:**
  - Bash script that:
    - Reads Terraform outputs (public IPs)
    - Uses `curl` to hit both servers
    - Prints ✅ OK or ❌ Down

---

## 4. Folder Structure

```text
.
├── main.tf                # Terraform providers (AWS + GCP) and basics
├── variables.tf           # Input variables (region, project ID, etc.)
├── terraform.tfvars       # Your actual values for variables
├── health_check.sh        # Bash health check script
├── aws/
│   └── ec2.tf             # AWS EC2 resources
└── gcp/
    └── compute.tf         # GCP Compute Engine resources
