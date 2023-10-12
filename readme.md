# Django Project Deployment on AWS LightSail Containers via GitHub Actions

This guide will walk you through setting up and deploying your Django project on AWS LightSail containers using GitHub Actions. This deployment strategy offers super easy deployment, high scalability, and eliminates the hassle of managing servers.

## Prerequisites packages installed
- [ ] Have Python3 installed
- [ ] run `brew install mysql` - in case you have don't have this
- [ ] run `pip3 install -r requirements.txt` to get all requirements for template

## Prerequisites hosting 

Before you start, make sure you have the following prerequisites:

- Clone this repository to your own Github account
- AWS account with LightSail service enabled and a 


## Steps

### 1. Configure AWS LightSail Container Service

- Log in to your AWS Management Console.
- Navigate to the LightSail container.
- Create a container service and configure it based on your project requirements.
- Note the name of your service (you'll need it later)
- Note the region of your service
- Write down your `service name` and your `region`

### 2. Set Up AWS Access Credentials

Generate AWS access credentials with the necessary permissions and store them securely. You can use AWS IAM for this purpose.
Plenty of tuturials on how to obtain this. At the end of this step you should have: 

`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`

In AWS lightsail create a storage bucket and obtain the: 
- `S3_SECRET_KEY`
- `S3_ACCESS_KEY`
-  `S3_AWS_STORAGE_BUCKET_NAME`

### 3. Update GitHub Repository Secrets

In your GitHub repository, go to `Settings` -> `Secrets` and add the following secrets:

- `AWS_ACCESS_KEY_ID`: Your AWS access key ID. from step 2
- `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key. from step 2
- `AWS_REGION`: Your AWS region (e.g., `us-east-1`). this must match what you did in step 1 
- `S3_AWS_STORAGE_BUCKET_NAME` - for file storage
- `S3_ACCESS_KEY` 
- `S3_SECRET_KEY`
- `DB_USER` 
- `DB_PASSWORD` 
- `DB_HOST`
- `DB_NAME`
- `DB_PORT` - for your SQL database. 
You can also use sqlite in which case you should change your settings.py file in django to do so. But I chose to use a SQL database since data will otherwise be lost if the container reboots. 
