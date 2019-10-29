## Introduction

This workshop will show you how to build your first fullstack serverless application using Amazon Web Services. You will look at all the tools and services required to create a web app using AWS services that don't require you to manage server infrastructure. 

If you've never heard of "Serverless" before I'll explain the benefits and drawbacks of moving the responsibility for the configuration and maintenance of servers to a provider like AWS. This workshop will have you working with several AWS services including: Amazon S3, Amazon DynamoDB, AWS Lambda, and AWS API Gateway to create your first fullstack Serverless Application.

# Outline

### [Setup - Instructor Checkoff Steps](/checkoff.md)

- Installing Node and npm
- Creating an AWS Account
- Setting up the Serverless Framework and Serverless Dashboard
- Deploying our first service

### [Demo Introduction](/demo-introduction.md)

- Seeing the final product we'll be building by the end of the workshop
- Reviewing the code samples for this workshop and where to get them

### [Deploying Your First Serverless API Service](/deploying-first-serverless-api-service.md)

- Deploying two HTTP API Endpoints built with AWS Lambda and API Gateway
- Integrating a DynamoDB Table to store data for our API
- Deploying our service through the Serverless Dashboard

### [Deploying Your First Serverless Frontend](/deploying-first-serverless-frontend.md)

- Installing and configuring a Serverless Framework Plugin
- Adding our deployed HTTP API endpoints to our website
- Deploying the website to Amazon S3

### [Adding Authentication to Our Frontend](/adding-authentication.md)

- Configuring our own Auth0 tenant
- First steps of adding authentication to our website
