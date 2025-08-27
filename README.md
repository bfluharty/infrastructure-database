# 📦 infra-database

This repository manages **database infrastructure** for our AWS environments, using **Amazon RDS** as the primary managed database service.

The goal of this repo is to provide a **centralized, consistent, and secure way** to provision, configure, and manage shared database infrastructure that may be used by multiple applications across different repositories.


## 🚀 Purpose

* Define and manage **Postgres RDS instances** as infrastructure-as-code.
* Enforce **best practices** for availability, durability, and security (e.g., backups, encryption, IAM).
* Provide a **single source of truth** for database resources used across the organization.
* Allow application teams to **consume outputs** (endpoints, credentials, etc.) without needing to manage database infra themselves.

## 📂 Repo Structure

```
infra-database/
├── README.md                # This file
├── template.yml             # CloudFormation/SAM template for RDS
├── modules/                 # (Optional) Reusable IaC modules (Terraform/CloudFormation/CDK)
├── environments/            # Environment-specific configs (dev, qa, prod)
│   ├── dev.yml
│   ├── qa.yml
│   └── prod.yml
└── ci-cd/                   # Deployment pipeline definitions (GitHub Actions / CodePipeline)
```

## ⚙️ How It Works

1. **Define Databases**
   Each environment specifies the RDS instances it needs (engine type, size, storage, backups, etc.).

2. **Deploy via CI/CD**
   Changes to the infra repo trigger pipelines that apply updates in AWS (CloudFormation, SAM, or Terraform).

3. **Expose Outputs**
   After deployment, the database **endpoint, port, and credentials location** (in AWS Secrets Manager or SSM Parameter Store) are shared with consuming applications.

## 🔑 Security & Access

* All credentials are managed via **AWS Secrets Manager / SSM**, never stored in code.
* Database access is restricted via **VPC security groups**.
* Automated **backups and snapshots** are enabled by default.
* Infrastructure changes require PR review and CI/CD approval.

## 🌍 Environments

We currently manage RDS infrastructure for the following environments:

* **Development** → lightweight, lower-cost instances
* **QA** → production-like configuration for testing
* **Production** → highly available, secure, and scalable setup

## 📜 Contribution Guidelines

* All changes must go through a **Pull Request**.
* PRs must pass **linting, validation, and security checks**.
* Include a **changelog entry** describing database changes.
* Coordinate with application teams before making breaking changes (e.g., DB version upgrades).

## 📈 Roadmap

* [ ] Add automated RDS snapshot lifecycle policies
* [ ] Add monitoring & alarms (CloudWatch, Datadog, etc.)
* [ ] Implement automated failover tests
