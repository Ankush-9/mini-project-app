# mini-project-app

CICD Pipeline Project (mini Project)
===============================================
Project name = Secure AWS CICD Pipeline for web application, using AWSCodePipeline

Summary:
We have our AWS Account.Now we are going to use AWS Code Pipeline.We are going to get the project from GitHub
We are going to use components in AWS like AWS CodeBuild, AWS CodeDeploy in S3 Bucket(static project) , CloudFront(CloudFront is used to reduce latency for different zone accesses)
I.e To get equal latency for access across the globe we use CloudFront
Optional ~ We can use Route53 to do domain mapping
Additionally we cans secure the entire app with the help of firewall

Steps:
==============================================
Create S3 Bucket
ACLs enabled or public access
Uncheck Block all public access
Under Properties —> Static Website Hosting —> edit—>enable Static website hosting and add index.html as default file
Now go to the Bucket —> Permissions —> Edit Bucket Policy —> 
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

Next up, We’ll be creating the CodePipeline
CodePipeline —> CodeBuild and CodeDeploy

—>CodeBuild -> Build Projects -> Create build project
	Name : Ankush-demo-app
	Default
	Source 1 - Primary —> Github

Setup Connections in Settings
Create a Connection to Github
——Pending———Theory—and——Practical——





