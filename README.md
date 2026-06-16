# Automated Portfolio Website Deployment using GitHub Actions and AWS S3

## Project Overview

This project demonstrates how to automate the deployment of a static portfolio website using **GitHub Actions** and **AWS S3 Static Website Hosting**.

Whenever changes are pushed to the GitHub repository, GitHub Actions automatically deploys the updated website files to an AWS S3 bucket, creating a simple CI/CD pipeline.

---

## Architecture

```text
Developer (VS Code)
        │
        ▼
     GitHub Repository
        │
        ▼
   GitHub Actions
        │
        ▼
     AWS S3 Bucket
        │
        ▼
  Static Portfolio Website
```

---

## Features

* Responsive Portfolio Website
* Automated Deployment using GitHub Actions
* AWS S3 Static Website Hosting
* Continuous Integration and Continuous Deployment (CI/CD)
* Secure AWS Authentication using GitHub Secrets
* Easy Maintenance and Updates

---

## Technologies Used

* HTML5
* CSS3
* JavaScript
* Git
* GitHub
* GitHub Actions
* AWS S3
* AWS IAM

---

## Project Structure

```text
portfolio-website/
│
├── index.html
├── style.css
├── script.js
│
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## Prerequisites

Before starting, ensure you have:

* AWS Account
* GitHub Account
* VS Code
* Git Installed
* AWS S3 Bucket
* IAM User with S3 Access

---

## AWS Configuration

### Step 1: Create an S3 Bucket

* Open AWS Console
* Navigate to S3
* Create a bucket
* Disable Block Public Access
* Enable Static Website Hosting

### Step 2: Create IAM User

* Navigate to IAM
* Create a new user
* Attach AmazonS3FullAccess policy
* Generate Access Key and Secret Key

---

## GitHub Secrets Configuration

Add the following secrets in:

```text
Repository Settings
→ Secrets and Variables
→ Actions
```

| Secret Name           | Description                   |
| --------------------- | ----------------------------- |
| AWS_ACCESS_KEY_ID     | AWS Access Key                |
| AWS_SECRET_ACCESS_KEY | AWS Secret Key                |
| AWS_REGION            | AWS Region (e.g., ap-south-1) |
| S3_BUCKET_NAME        | S3 Bucket Name                |

---

## GitHub Actions Workflow

The workflow automatically triggers whenever code is pushed to the `main` branch.

### Workflow File

```yaml
name: Deploy Portfolio Website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Upload Files to S3
        run: |
          aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete \
          --exclude ".git/*" \
          --exclude ".github/*"
```

---

## Deployment Steps

1. Clone the repository

```bash
git clone <repository-url>
```

2. Navigate to the project folder

```bash
cd portfolio-website
```

3. Make changes to website files

4. Commit changes

```bash
git add .
git commit -m "Updated website"
```

5. Push changes

```bash
git push origin main
```

6. GitHub Actions automatically deploys the website to AWS S3.

---

## CI/CD Workflow

```text
Code Change
     │
     ▼
Git Push
     │
     ▼
GitHub Actions Triggered
     │
     ▼
AWS Authentication
     │
     ▼
S3 Deployment
     │
     ▼
Website Updated
```

---

## Learning Outcomes

Through this project, I gained hands-on experience with:

* Version Control using Git and GitHub
* CI/CD Pipeline Automation
* GitHub Actions Workflow Creation
* AWS S3 Static Website Hosting
* IAM User and Access Management
* Secure Secret Management in GitHub

---

## Future Enhancements

* Deploy using CloudFront CDN
* Add Custom Domain with Route 53
* Implement HTTPS using AWS Certificate Manager
* Add Portfolio Contact Form
* Integrate Monitoring and Logging

---

## Author

**Ashish Lanjewar**

Aspiring DevOps Engineer

LinkedIn: linkedin.com/in/ashishlanjewar

GitHub: github.com/ashish-devops10
