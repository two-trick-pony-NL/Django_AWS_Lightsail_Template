# Django Project Deployment on AWS LightSail Containers via GitHub Actions
## Why: 
Setting up django for production is hard! Using this template will give you a easy deployment that comes out of the box with: 
- 🐳 Container service (Easily scale both horizontally and vertically in AWS lightsail)
- 🔐 SSL Certificate on connection
- 🦺 Safety: if your build fails -> the old container will stay live so you site won't go down
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
- [ ] fill in the `core/.env` file with your app's details. I provided a sample in the `core` folder
- [ ] run `python3 manage.py runserver` to check if the app is working on your local machine


## Steps

### 0. 
- I assume you have cloned the repo to your github account
- You have a AWS account and can log in to http://lightsail.aws.amazon.com 

### 1. Configure AWS LightSail Container Service

- Log in to your AWS on http://lightsail.aws.amazon.com
- Create a container service and name it `djangoapp` and pick a region you desire. 
- Note the region of your service
<img width="1022" alt="Schermafbeelding 2023-10-12 om 23 58 58" src="https://github.com/two-trick-pony-NL/Django_AWS_Lightsail_Template/assets/71013416/29b491f5-e837-4b93-8f2c-14b0e7e9be5b">
<img width="1022" alt="Schermafbeelding 2023-10-12 om 23 59 38" src="https://github.com/two-trick-pony-NL/Django_AWS_Lightsail_Template/assets/71013416/3b7e85df-04ea-49d1-83c5-8ede2810d8d9">



### 2. Set Up AWS Access Credentials

Generate AWS access credentials with the necessary permissions and store them securely. You can use AWS IAM for this purpose.
Plenty of tuturials on how to obtain this. At the end of this step you should have: 

`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`

In AWS lightsail create a storage bucket and obtain the: 
- `S3_SECRET_KEY`
- `S3_ACCESS_KEY`
- `S3_AWS_STORAGE_BUCKET_NAME`

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

When you're done it should look like this: 

<img width="956" alt="Schermafbeelding 2023-10-12 om 23 29 52" src="https://github.com/two-trick-pony-NL/Django_AWS_Lightsail_Template/assets/71013416/fd8cdc56-5516-4884-92db-dc9b1760b2cd">



### 4. Update your app

- Now you can update your app locally and update it to your hearts desire
- Once you commit to main, github action will trigger
- That looks like this:
<img width="425" alt="Schermafbeelding 2023-10-12 om 23 30 24" src="https://github.com/two-trick-pony-NL/Django_AWS_Lightsail_Template/assets/71013416/bf41300f-bc1e-4031-9d4a-28b434a673be">
- Once the deployment completes your lightsail dashboard should look like this:
  <img width="953" alt="Schermafbeelding 2023-10-12 om 23 31 10" src="https://github.com/two-trick-pony-NL/Django_AWS_Lightsail_Template/assets/71013416/2153f467-e6d6-467c-ad00-21d654149a04">
  - including the URL to your new container. You can set your own domain name from the lightsail dashboard later. 
- you might need to add the AWS host to your `allowed_hosts` in `core/settings.py` simply paste the URL given by Lightsail e.g: djangoapp.vdotvo9a4e2a6.eu-central-1.cs.amazonlightsail.com 
