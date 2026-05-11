# Secure AWS CI/CD Pipeline for Static Web Application

A production-style CI/CD pipeline project built on AWS using AWS CodePipeline, AWS CodeBuild, Amazon S3, and CloudFront for automated deployment of a static web application directly from GitHub.

---

# Project Overview

This project demonstrates how to build a secure and scalable CI/CD pipeline on AWS for hosting and deploying a static web application.

The pipeline automatically fetches source code from GitHub, builds the application using AWS CodeBuild, and deploys the generated artifacts to an Amazon S3 bucket configured for static website hosting. CloudFront is integrated to provide low-latency global content delivery.

The project simulates a real-world DevOps workflow using AWS managed services.

---

# Architecture

```text
Developer Pushes Code to GitHub
            │
            ▼
     AWS CodePipeline
            │
            ▼
      AWS CodeBuild
            │
            ▼
    Amazon S3 Deployment
            │
            ▼
      AWS CloudFront
            │
            ▼
      End Users Access Website
```

---

# AWS Services Used

| Service | Purpose |
|----------|----------|
| AWS CodePipeline | Automates CI/CD workflow |
| AWS CodeBuild | Builds the application |
| Amazon S3 | Hosts static website files |
| AWS CloudFront | Global CDN for low latency delivery |
| IAM | Role-based access management |
| GitHub | Source code repository |
| Route53 *(Optional)* | Domain mapping |
| AWS WAF *(Optional)* | Web application firewall |

---

# Features

- Automated CI/CD pipeline
- GitHub integration with AWS
- Automatic deployment on code push
- Static website hosting using S3
- Global content delivery using CloudFront
- IAM role-based security
- Scalable and serverless architecture
- Optional domain mapping using Route53
- Optional firewall protection using AWS WAF

---

# Project Workflow

1. Developer pushes code to GitHub repository  
2. AWS CodePipeline detects repository changes  
3. CodeBuild starts build process using `buildspec.yml`  
4. Build artifacts are generated  
5. AWS deploys files to Amazon S3 bucket  
6. CloudFront distributes content globally  
7. Users access the deployed application with reduced latency  

---

# Step-by-Step Setup

## 1. Create S3 Bucket

- Create a new S3 bucket
- Enable ACLs/Public Access
- Disable:
  - `Block all public access`
- Enable:
  - `Static Website Hosting`
- Set:
  - `index.html` as default document

### Bucket Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::ankush-mini-project/*"
    }
  ]
}
```

---

# 2. Configure AWS CodeBuild

## Create Build Project

Navigate to:

```text
AWS CodeBuild → Build Projects → Create Build Project
```

### Configuration

| Setting | Value |
|----------|--------|
| Project Name | Ankush-demo-app |
| Source Provider | GitHub |
| Build Type | Single Build |
| OS | Amazon Linux |
| Buildspec | Use buildspec.yml |
| Service Role | Create New Service Role |

---

# 3. Connect GitHub to AWS

Navigate to:

```text
AWS Settings → Connections → Create Connection
```

### Configuration

| Setting | Value |
|----------|--------|
| Provider | GitHub |
| Connection Name | AWS-Github-Connection |

### Steps

- Connect GitHub Account
- Install AWS Connector App
- Grant Repository Permissions
- Complete Connection Setup

Enable webhook integration to trigger builds automatically whenever new code is pushed.

---

# 4. Configure IAM Permissions

After CodeBuild project creation:

```text
IAM → Roles → CodeBuild Service Role
```

Add the following permission:

```text
CloudFrontFullAccess
```

This allows pipeline invalidation and CDN-related actions if required.

---

# 5. Create AWS CodePipeline

Navigate to:

```text
AWS CodePipeline → Create Pipeline
```

### Pipeline Configuration

| Setting | Value |
|----------|--------|
| Pipeline Type | Custom Pipeline |
| Pipeline Name | Ankush-webapp-pipeline |
| Execution Mode | Queued |
| Service Role | New Service Role |

---

# 6. Configure Source Stage

| Setting | Value |
|----------|--------|
| Source Provider | GitHub |
| Connection | AWS-Github-Connection |
| Branch | main |

---

# 7. Configure Build Stage

| Setting | Value |
|----------|--------|
| Build Provider | AWS CodeBuild |
| Project Name | Ankush-demo-app |

---

# 8. Configure Deploy Stage

| Setting | Value |
|----------|--------|
| Deploy Provider | Amazon S3 |
| Target Bucket | Your S3 Bucket |
| Extract Files Before Deploy | Enabled |

---

# buildspec.yml Overview

The `buildspec.yml` file controls the build lifecycle in AWS CodeBuild.

Typical phases include:

- Install dependencies
- Build project
- Prepare deployment artifacts
- Upload generated files

Example structure:

```yaml
version: 0.2

phases:
  install:
    commands:
      - echo "Installing dependencies"

  build:
    commands:
      - echo "Building application"

artifacts:
  files:
    - '**/*'
```

---

# CloudFront Integration

CloudFront is used to distribute website content globally using edge locations.

## Benefits

- Reduced latency
- Faster website loading
- Better global accessibility
- Improved caching performance
- Enhanced scalability

---

# Security Considerations

This project follows secure DevOps practices by implementing:

- IAM role-based access control
- Managed AWS services for reduced operational overhead
- Secure GitHub integration using AWS Connections
- Controlled deployment permissions
- Optional AWS WAF protection for enhanced web security
- CloudFront secure content delivery
- Automated CI/CD workflow with centralized pipeline management

These practices help improve application reliability, deployment security, and infrastructure scalability while following modern DevOps standards.

---

# Optional Enhancements

Future improvements that can be added:

- HTTPS using ACM Certificates
- Custom Domain using Route53
- AWS WAF Integration
- Multi-Environment Deployment
- Terraform Automation
- Monitoring using CloudWatch
- Slack/Email Notifications
- Blue-Green Deployment Strategy

---

# Learning Outcomes

By completing this project, you will understand:

- CI/CD pipeline architecture
- AWS DevOps services integration
- Automated deployments
- Static website hosting
- CDN concepts using CloudFront
- IAM role management
- GitHub to AWS workflow automation

---

# Use Case

This setup is ideal for:

- Portfolio websites
- Static frontend applications
- Landing pages
- Documentation websites
- React/Vue static builds
- DevOps learning projects

---

# Author

Ankush Walia

---

# Conclusion

This project demonstrates how modern DevOps pipelines can automate application deployment using AWS managed services. It provides a scalable, secure, and globally accessible deployment workflow for static web applications while following industry-standard CI/CD practices.
