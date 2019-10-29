# Demo Introduction

## The Frontend

In this workshop, we'll be building out Serverless Jams - a website dedicated to voting on some of the best coding music out there. Here's a screenshot:

![Serverless Jams](/images/serverlessjams-screenshot.png)

I'll provide a pre-built website using some basic HTML, CSS, and JavaScript that you will integrate with several HTTP APIs. You'll also learn how to deploy the service and see it live and hosted on AWS.

## The Backend

To make this website work, we'll be creating two HTTP API endpoints. One will allow you to vote for a song using a song id. The other endpoint will retrieve the data for the three songs we have selected already. But how are we making that all work? Let's take a look at how the data will flow through our application:

1. The data will hit one of two HTTP API endpoints created with AWS API Gateway
2. The API Gateway endpoint will pass the data along to a corresponding AWS Lambda function
3. The Lambda function will process that data and then communicate with an Amazon DynamoDB table
4. Data will be stored or retrieved from DynamoDB depending on the API Gateway endpoint used
5. The Lambda function will then return a result back to API Gateway
6. API Gateway will return a response to the HTTP request
7. The application will process the request and update the UI

Here's a visual:

![A diagram demonstrating the flow described above](/images/backend-diagram.png)

# Where's the Code?!

While we work on the workshop we'll be trying to build up to the final product bit by bit so we can understand everything in sequence. But, we'll slowly build towards the final product [here](https://github.com/fernando-mc/serverlessjams). So go ahead and clone that repository now.

Keep in mind that, in the long run, several of the values inside of `serverless.yml`, `app.js` and `auth_config.json` will need to change in order for you properly setup your own application.

### [Next - Deploying Your First Serverless API](deploying-first-serverless-api.md)