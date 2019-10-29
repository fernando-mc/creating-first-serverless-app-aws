# Adding Authentication to Our Frontend

Congrats! You're up and running with a semi-functional website (I hope)!

Possibly you have just one problem, when you deployed the site to Amazon S3 the authentication broke. Darn! What's up with that?

Well, when I provided my Auth0 token (that is meant to be exposed on the frontend). I also configured it so that it could be used with `localhost:3000` as the domain. I didn't say that all of your Amazon AWS S3 Static hosting domains could use it though!

For you to do that, you'll need to create your own Auth0 account. If you followed the optional extra steps in the [checkoff](/checkoff.md) you should be almost ready. If not, don't worry. I'll recap:

- Create an [Auth0 Account](https://auth0.com/)
    - Create a tenant domain in the US
    - Click "Create Application"
    - Click "Single Page Web Applications" and "create"
    - Visit the Settings for your app
    - Copy the Domain and Client ID
    - Add an allowed callback url of http://localhost:3000
    - Add ANOTHER allowed callback url of the domain of your deployed website

Make sure to save all your settings and then take the Auth0 domain and the client id values and go find the `auth_config.json` file in your frontend code and replace the values I've provided with your own. Make sure to save and try testing the application locally again, hopefully you'll have to sign up for another account and do so using your new Auth0 tenant. 

To be sure it works, rerun `serverless client deploy` and test the application at your deployed URL.

And hopefully... You have a functioning application! If not, I've failed you horribly and would appreciate any PR fixes to this tutorial or my code!

### [Previous - Deploying Your First Serverless Frontend](deploying-first-serverless-frontend.md)