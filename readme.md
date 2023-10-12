# Django Project Deployment on AWS LightSail Containers via GitHub Actions

This guide will walk you through setting up and deploying your Django project on AWS LightSail containers using GitHub Actions. This deployment strategy offers super easy deployment, high scalability, and eliminates the hassle of managing servers.

## Prerequisites

Before you start, make sure you have the following prerequisites:

- AWS account with LightSail service enabled
- GitHub repository for your Django project
- Docker installed on your local machine

## Steps

### 1. Configure AWS LightSail Container Service

- Log in to your AWS Management Console.
- Navigate to the LightSail service.
- Create a container service and configure it based on your project requirements.

### 2. Set Up AWS Access Credentials

Generate AWS access credentials with the necessary permissions and store them securely. You can use AWS IAM for this purpose.

### 3. Update GitHub Repository Secrets

In your GitHub repository, go to `Settings` -> `Secrets` and add the following secrets:

- `AWS_ACCESS_KEY_ID`: Your AWS access key ID.
- `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key.
- `AWS_DEFAULT_REGION`: Your AWS region (e.g., `us-east-1`).

### 4. Create GitHub Actions Workflow

Create a `.github/workflows/main.yml` file in your repository with the following content:

```yaml
name: Django AWS LightSail Deployment

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Set Up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8

    - name: Install Dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Deploy to AWS LightSail
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_DEFAULT_REGION: ${{ secrets.AWS_DEFAULT_REGION }}
      run: |
        # Add deployment script or commands here
