# Creating Your First Fullstack Serverless Application on AWS

## Introduction

This workshop will show you how to build your first fullstack serverless application using Amazon Web Services. You will look at all the tools and services required to create a web app using AWS services that don't require you to manage server infrastructure. 

If you've never heard of "Serverless" before I'll explain the benefits and drawbacks of moving the responsibility for the configuration and maintenance of servers to a provider like AWS. This workshop will have you working with several AWS services including: Amazon S3, Amazon DynamoDB, AWS Lambda, and AWS API Gateway to create your first fullstack Serverless Application.

# Outline

## [Setup - Instructor Checkoff Steps](/checkoff.md)


http-server -p 3000

## Outline

- About me (1 min)
    - Who I am, what I do
    
- Overview of Serverless (5 min)
    - What is Serverless?
    - The rise of Serverless Applications
    - Serverless Benefits
    - Serverless Limitations

- Setup Steps (20 min)
    - Creating an AWS Account
    - Installing and configuring the AWS CLI
    - Accessing the AWS Console
    - Accessing the example code for the workshop

- Step 1: Creating Our Database Layer with DynamoDB (15 min)
    - Relational (SQL) vs. NoSQL
    - What is DynamoDB?
    - Interacting with DynamoDB
    - DynamoDB drawbacks and benefits
    - Creating and interacting with a DynamoDB Table

- Step 2: Creating our Application Logic Code in AWS Lambda (12 min)
    - What is AWS Lambda
    - Working with Lambda Functions
    - Using Boto3 and Python to interact with DynamoDB

- Step 3: Creating an API for Our Application with the AWS API Gateway (12 min)
    - What is API Gateway?
    - Creating an API Gateway API that integrates with our Lambda Function

- Step 4: Creating a Static Site with Amazon S3 (12 min)
    - What are static sites?
    - How can we use Amazon S3 to host a static site?
    - Review static site code CRUD app
    - Minor modifications to site code
    - Creating an S3 Bucket
    - Upload code to Amazon S3

- Reviewing and extending our new application (12 min)
    - Review 
        - See it live at the S3 static site domain
        - See the API Gateway handle CRUD requests
        - See logs of Lambda Function processing our request
        - See the DynamoDB table updated with new data
    - Where to go now?
        - Consider adding a custom domain with Route 53
        - Add caching and HTTPS on the custom domain with CloudFront and the AWS Certificate Manager
        - Add authentication with Amazon Cognito
        - Describe this application with CloudFormation to have the infrastructure stored as code
        - Look at frameworks like the Serverless Framework that can help speed up this process 

- Closing (5 min)
    - Thank yous
    - More suggestions for other tutorials as next steps
    - Had an issue with something?
        - Use a link to CloudFormation code
        - Used to deploy the entire demo application
        - Review later in your AWS account

