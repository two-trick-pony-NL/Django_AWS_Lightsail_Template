# Django Project Deployment on AWS LightSail Containers via GitHub Actions
## Why: 
Setting up django for production is hard! Using this template will give you a easy deployment that comes out of the box with: 
- 🐳 Container service (Easily scale both horizontally and vertically in AWS lightsail)
- 🔐 SSL Certificate on connection
- 🌎 Nginx reverse proxy integrated with uwsgi no set up required
- 🗂 S3 file storage configured out of the box ready to use in django
- 🤐 Environment secrets tucked away in your repository secrets (so easy to collaborate)
- 🏎 From code commit to deployed in less than 5 minutes
- 🤑 Serverless deployment for < $7 per month

## How: 
- Ever time you commit code to branch `main` --> You trigger a deploy to a new lightsail container automatically
- This process is fully automated if you provide the correct credentials in your Github Secrets

## What can I do with this?
- You can build anything you like, without the hassle of setting up reverse proxies, docker containers, updating servers, ssl Sertificate
- Just go wild on your app without the hassle of hosting. 

# Installation


## Prerequisites and testing locally
- [ ] Have Python3 installed
- [ ] run `brew install mysql` - in case you have don't have this
- [ ] run `pip3 install -r requirements.txt` to get all requirements for template
- [ ] fill in the `core/.env` file with your app's details
- [ ] run `python3 manage.py runserver` to check if the app is working on your local machine

## Prerequisites hosting 

Before you start, make sure you have the following prerequisites:

- Clone this repository to your own Github account - so we can leverage github actions
- AWS account with LightSail service enabled and a container service explicitly called `djangoapp` - the build script depends on your app having this name. You can update it later by using find and replace and rebuilding your containers. 


## Steps

### 1. Configure AWS LightSail Container Service
- Log in to your AWS Management Console.
- Navigate to the LightSail container.
- Create a container service and name it `djangoapp` and pick a region you desire. 
- Note the region of your service

### 2. Set Up AWS Access Credentials

Generate AWS access credentials with the necessary permissions and store them securely. You can use AWS IAM for this purpose.
Plenty of tuturials on how to obtain this. At the end of this step you should have: 

`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`

In AWS lightsail create a storage bucket and obtain the: 
- `S3_SECRET_KEY`
- `S3_ACCESS_KEY`
- `S3_AWS_STORAGE_BUCKET_NAME`
- 

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
