
# Lab M5.06 - Deployment Strategies (Blue/Green)
 
## Architecture
 
Two S3 static website buckets serve as deployment targets:
- **Blue** — `deploy-lab-blue.s3-website-us-east-1.amazonaws.com`
- **Green** — `deploy-lab-green.s3-website-us-east-1.amazonaws.com`
 
Only one is "active" at a time, tracked by `deployment.json`.


Start Here: Fork, Clone, and Submit

Fork the lab repository to your GitHub account.

Clone your fork locally:

git clone https://github.com/MaryaAhmadi/ce-lab-infrastructure-testing.git
cd ce-lab-infrastructure-testing

Complete the lab instructions, saving all work (files, screenshots, notes) in this repository.

Stage, commit, and push your changes:

git add .
git commit -m "Complete lab M5.05"
git push origin main

Open a Pull Request (PR) from your fork to the original lab repository.

Copy the PR URL and submit it in the Lab Submission field on the Student Portal.

## 📋 Lab Overview

This lab focuses on implementing comprehensive testing for infrastructure code, including:

Syntax validation

Linting

Security scanning

Compliance and custom checks

You will build a multi-layer testing strategy for Terraform code to ensure consistency, security, and compliance.

## 🎯 Learning Objectives

By the end of this lab, you will be able to:

Implement infrastructure testing frameworks

Configure automated validation in CI/CD pipelines

Run Terraform validation (terraform validate) and linting (tflint)

Perform security scanning using Checkov

Create and run custom validation tests for naming conventions, tagging, and plan verification

## 📁 Repository Structure
ce-lab-infrastructure-testing/
├── .github/
│   └── workflows/
│       └── test-infrastructure.yml
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
├── scripts/
│   ├── validate-conventions.sh
│   ├── validate-plan.sh
│   └── install-hooks.sh
├── tests/
│   ├── terraform_test.go
│   └── compliance_test.sh
├── .tflint.hcl
├── .pre-commit-config.yaml
├── README.md
└── .gitignore

## Architecture

The deployment uses two S3 static website buckets as targets:

Blue — http://deploy-lab-maryam-ironhack-blue.s3-website-us-east-1.amazonaws.com

Green — http://deploy-lab-maryam-ironhack-green.s3-website-us-east-1.amazonaws.com

At any time, only one environment is active, tracked via deployment.json.


## Workflows
Deploy & Switch (.github/workflows/deploy.yml)

Reads deployment.json to determine the inactive environment.

Deploys new content to the inactive bucket.

Performs a health check (expects HTTP 200).

Switches active_environment in deployment.json.

Commits the updated deployment state back to the repository.

Rollback (.github/workflows/rollback.yml)

Reads deployment.json to identify the currently active environment.

Switches back to the previous environment (no redeployment needed).

Records the rollback reason in the deployment history.

Commits the updated state back to the repository.


##Deployment State (deployment.json)

This file serves as the single source of truth, tracking:

Active environment (blue or green)

Current version deployed

Deployer (github.actor)

Timestamp of deployment

Full history of deployments and rollbacks


## Key Learnings

Blue/Green deployments eliminate downtime — traffic switches instantly.

The inactive environment is always ready for the next deployment.

Rollback is instant — simply switch the pointer back.

Deployment history provides a full audit trail for traceability.


## ✅ Submission Requirements

Complete the lab as described and save your work in this repository:

Testing Workflows

Terraform validation

TFLint configuration and execution

Security scanning with Checkov

Custom compliance tests

Infrastructure Code

Working Terraform configuration

Proper resource configuration

Test Documentation

Testing strategy explanation

Test coverage documentation
