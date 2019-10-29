# Deploying Your First Serverless Frontend

#### [Outline](README.md)

### Goals

- Installing and configuring a Serverless Framework Plugin
- Adding our deployed HTTP API endpoints to our website
- Deploying the website to Amazon S3

## Getting Our Website Code and Updating Our Endpoints

I'm not going to make you create a frontend from scratch so... the entire frontend for the application can be found [here](https://github.com/fernando-mc/serverlessjams/tree/master/frontend). Go ahead and copy the files from the final demo to a new `frontend` directory. 

We will need to update lines 7 and 8 of the `app.js` file in the `js` folder to use them inside of our site. Basically, our site should be firing HTTP requests to those endpoints to power the voting features it uses.

Other than that, we're just using Semantic UI and some Spotify embeds to make the site look pretty.

After you've saved and updated all the files, run a local webserver to take a look at your project. To get authentication I've already integrated without too much work, make sure to run it on `localhost:3000`. 

Try running one of these in the `frontend` directory to load it up:

- With Python 2 `python -m SimpleHTTPServer 3000` 
- With Python 3: `python3 -m http.server`
- With npm and http-server: `npm install -g http-server && http-server -p 3000`

After this, try visiting [http://localhost:3000](http://localhost:3000) and interacting with the site! See If you can vote on the songs! See if it updates and refreshes. If you want to join my personal mailing list you can also sign up using the authentication and I promise to send you copious amounts of tutorials. Try signing in with Google auth to see your avatar brought in (more on all the auth later).

Also notice that the voting options appear and disappear depending on the signed in status of the application.

## Installing Serverless Finch and Updating serverless.yml

Now that we've updated our website we need to deploy it! Let's start by installing a Serverless Framework plugin called `serverless-finch` to deploy static websites like this.

Run `npm install serverless-finch --save-dev` in the same directory as `serverless.yml`.

Then, open back up `serverless.yml` and we'll add two new top-level sections. First, you'll add a `plugins` section that looks like this:

```yaml
plugins:
  - serverless-finch
```

This section will allow the `serverless-finch` plugin to integrate with commands from the Serverless Framework and let the Framework CLI know where to look for the plugin. Next, you'll add a `custom` section:

```yaml
custom:
  client:
    bucketName: serverlessjams-lisa19-YOURNAME-YOURFAVEANIMAL
    distributionFolder: frontend
    errorDocument: index.html
```

This custom section will allow you to specify some configuration for the `serverless-finch` plugin so it can deploy your frontend. Specifically, it will create an S3 bucket for you and configure a static site with Amazon S3 Static site hosting. Then it will pop out the deployment location so you can view it on the public internet.

The `bucketName` you use will have to be globally unique, so if Mike A and Mike B in this workshop both really like Unicorns then one of you is gonna want to pick another animal.

The `distributionFolder` part will reference all our frontend code in the `frontend` directory. 

The `errorDocument` section will simply allow us to redirect folks to our homepage if some other page throws an error or doesn't exist. Be default, `index.html` is the default entry point for static sites like this.

With that all configured, we can run `serverless client deploy` and see our new website! Nice work!

If you notice the voting parts missing or the Auth0 integration failing, don't worry. We'll talk about that in the next section!

### [Previous - Deploying Your First Serverless API Service](deploying-first-serverless-api-service.md)

### [Next - Adding Authentication to Our Frontend](adding-authentication.md)