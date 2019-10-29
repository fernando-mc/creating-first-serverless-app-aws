# Deploying Your First Serverless API Service

### Goals

- Deploying two HTTP API Endpoints built with AWS Lambda and API Gateway
- Integrating a DynamoDB Table to store data for our API
- Deploying our service through the Serverless Dashboard

In this section, we'll deploy out a serverless HTTP API service with two different endpoints. One for recording vote counts on a song and one for getting vote counts back. Let's get started!

## serverless.yml

First, we'll need to create a new service!

Run `serverless` and go through the steps to create a new Python service called `serverless-jams`. I put mine in the application called `serverlessjams` which happens to be in my Serverless Dashboard organization called `fernando`.

### Serverless Dashboard Config

This initial setup should give me a basic serverless service that has a few config values similar to this in it:

```yaml
org: fernando
app: serverlessjams
service: serverless-jams
```

Leave the org, app, and service values that are setup in your `serverless.yml`. Those will allow you to deploy using your Serverless Dashboard account. 

### Provider Section Configuration

Next, we'll setup some service-level configuration in the provider section. The first few lines are simply to pick a cloud provider, setup a language runtime, and select a region.

```yaml
provider:
  name: aws
  runtime: python3.7
  region: us-east-1
  environment:
    DYNAMODB_TABLE: ${self:service}-${opt:stage, self:provider.stage}-voteCounts
  iamRoleStatements:
    - Effect: Allow
      Action:
        - dynamodb:Scan
        - dynamodb:PutItem
        - dynamodb:UpdateItem
      Resource: "arn:aws:dynamodb:${opt:region, self:provider.region}:*:table/${self:provider.environment.DYNAMODB_TABLE}"
```

The `environment` section however, is going to setup an environment variable called DYNAMODB_TABLE that we can later use in our code to get our table to interact with. It will be generated on deployment to include the name of the service, the stage we're deploying to, and the name of the table. The final result will look something like: `serverless-jams-dev-voteCounts`.

The `iamRoleStatements` section will allow us to setup the permissions our service will require - it will specifically allow our service to take a subset of actions on the table we create to add and update items as well as reading them from the table in bulk.

### Functions

Below the `provider` section, we'll need to configure a `functions` section. This section will allow us to reference the code that powers our two different HTTP APIs and setup the appropriate config for AWS API Gateway.

```yaml
functions:
  recordSongVote:
    handler: backend/record_song_vote.handler
    events:
      - http:
          path: song/vote
          method: post
          cors: true
  getSongVoteCounts:
    handler: backend/get_song_vote_counts.handler
    events:
      - http:
          path: votes
          method: get
          cors: true
```

Each of these functions is given a name and a `handler` reference. The handler reference for `recordSongVote` for example will tell us to look for a file called `record_song_vote.py` inside of a `backend` folder. It will also tell us to look for a `handler` function in that file to run with some event input.

The event input is then setup in the `events` section. The above configuration tells us that these functions should be triggered by `http` events and specifies the URL path and HTTP Method to be used. It also takes care of configuring Cross Origin Resource Sharing for these APIs. Behind the scenes, this configuration will allow us to connect all the disparate AWS resources together and deploy the API.

### The Resources Section - Our DynamoDB Table

```yaml
resources:
  Resources:
    usersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: ${self:provider.environment.DYNAMODB_TABLE}
        AttributeDefinitions:
          - AttributeName: songName
            AttributeType: S
        KeySchema:
          - AttributeName: songName
            KeyType: HASH
        ProvisionedThroughput:
          ReadCapacityUnits: 1
          WriteCapacityUnits: 1
```

Finally, we create our DynamoDB table. This configuration allows us to create a table with a limited capacity of approximately one read and write per second (though in reality we get some burst capacity for free). It also sets up a key to use for the items in the table.

## Setting up Our Function Code

Now, we just need to setup our function code. Make sure they live in a directory called `backend` that is right next to your `serverless.yml` file. If needed, just refer to the final version of the project. 

The first function will handle getting back all the data from the DynamoDB table and returning it:

```python
# get_song_vote_counts.py
import boto3
import os
import json

dynamodb = boto3.client('dynamodb')


def handler(event, context):
    result = dynamodb.scan(
        TableName=os.environ['DYNAMODB_TABLE']
    )
    song_votes = []
    for item in result["Items"]:
        song_votes.append({
            "songName": item["songName"]["S"],
            "votes": item["votes"]["N"]
        })
    response = {
        "statusCode": 200,
        "headers": {"Access-Control-Allow-Origin":"*"},
        "body": json.dumps(song_votes)
    }
    return response
```

The second function will allow us to increment the vote counts for each song we vote on:

```python
# record_song_vote.py
import boto3
import os
import json

dynamodb = boto3.client('dynamodb')


def handler(event, context):
    song_name = json.loads(event['body'])['songName']
    result = dynamodb.update_item(
        TableName=os.environ['DYNAMODB_TABLE'], 
        Key={
            'songName':{'S': song_name }
        },
        UpdateExpression='ADD votes :inc',
        ExpressionAttributeValues={
            ':inc': {'N': '1'}
        },
        ReturnValues="UPDATED_NEW"
    )
    response = {
        "statusCode": 200,
        "headers": {"Access-Control-Allow-Origin":"*"},
        "body": json.dumps({"votes" : result["Attributes"]["votes"]["N"]})
    }
    return response
```

When you're done creating these two files and updating your `serverless.yml` go ahead and run `serverless deploy` in your terminal! This should deploy the entire service and provide you with two API Endpoint URLs.

### [Previous - Demo Introduction](demo-introduction.md)

### [Next - Deploying Your First Serverless Frontend](deploying-first-serverless-frontend.md)
