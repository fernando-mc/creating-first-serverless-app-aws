# Checkoff Steps

#### [Outline](README.md)

Because this workshop is limited on time please make sure to check off these steps as soon as possible before the start of the workshop. If you have any questions you can get in touch with Fernando through any of the methods listed [here](https://www.fernandomc.com/contact). During the workshop, just ask him for help.

## Checkoff Steps:

1. [Create an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
2. [Sign into the AWS Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html)
3. [Create a Serverless Dashboard account](https://dashboard.serverless.com)
4. [Install Node.js and npm](https://nodejs.org/en/download)
5. Install or update the Serverless Framework: 
    - Install: `npm install -g serverless`
    - Update: `npm update -g serverless`
6. Setup an AWS Access Role in the [Serverless Dashboard](https://dashboard.serverless.com)
    - Sign into your AWS Account and the Serverless Dashboard in the same browser
    - Follow the steps under "Link your AWS Account" [here](https://serverless.com/framework/docs/dashboard/access-roles#link-your-aws-account) to connect your Serverless Dashboard account to AWS (you'll need to start inside the [Serverless Dashboard](https://dashboard.serverless.com))
7. I'd suggest doing the following to save yourself some time on the next step:
    - If possible, set Chrome or Firefox as default browsers (there are possible issues with Safari)
    - Temporarily disable any extensions that block JavaScript (e.g. NoScript) or and overzealous adblockers (we'll be doing some authentication calls to Auth0 that I've seen a NoScript extension block before)
    - You can turn your adblockers and NoScript back on as soon as the credentials are set locally on your machine after you login.
8. Run `serverless login` from your terminal. This should open up a browser window that asks you to sign in to the Serverless Dashboard. When you finish that process the terminal prompt should automatically move on. If this process fails, or you see error messages around authentication later on try these steps instead:
    - Login to the Serverless Dashboard
    - Go to the top right corner and click on the dropdown near your organization name
    - Click "Personal Access Keys"
    - Create an Access Key
    - Set an environment variable on your machine called `SERVERLESS_ACCESS_KEY`
    - Keep going as normal
9. Run `serverless` from your terminal and complete the prompts. Make sure to select your serverless dashboard account. 
10. When the process is finished, you should change directories into your new service directory with `cd your-service-name`.
11. Checkoff time! When you're done with these steps please run `serverless deploy` and let the instructor see the output. If you accidentally clear the screen too soon you can run `serverless info`.

Optional bonus step - Create an [Auth0 Account](https://auth0.com/)
    - Create a tenant domain in the US
    - Click "Create Application"
    - Click "Single Page Web Applications" and create
    - Visit the Settings for your app
    - Copy the Domain and Client ID
    - Add an allowed callback url of http://localhost:3000


### [Next - Demo Introduction](demo-introduction.md)

### [Previous - Outline](README.md)