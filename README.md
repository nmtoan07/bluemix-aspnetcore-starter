# Getting started with ASP.NET Core 1.0 on Bluemix on Visual Studio 2017
This guide will take you through the steps to get started on Bluemix with the help of a sample application. In 10 minutes or less, you’ll learn to:
- Set up a development environment
- Download sample code
- Run the application locally
- Run the application on Bluemix Cloud Foundry
- Add a Bluemix Database service
- Connect to the database from your local application


## Prerequisites

You'll need the following:
* [Bluemix account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI](https://github.com/cloudfoundry/cli#downloads)
* [Git](https://git-scm.com/downloads)
* Install .NET Core SDK and Runtime from the [download page](https://www.microsoft.com/net/download/core) instructions.

## 1. Clone the sample app

Now you're ready to start working with the app. Clone the repository and change to the directory where the sample app is located.
  ```
git clone https://github.com/nmtoan07/bluemix-aspnetcore-starter
cd get-started-aspnet-core
  ```

## 2. Run the app locally
{: #run_locally}

Run the app.
  ```
cd src/GetStartedDotnet
dotnet restore
dotnet run
  ```

View your app at: http://localhost:5000/

## 3. Prepare the app for deployment

To deploy to Bluemix, it can be helpful to set up a manifest.yml file. One is provided for you with the sample. Take a moment to look at it.

The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. In this manifest.yml **random-route: true** generates a random route for your app to prevent your route from colliding with others.  You can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice. [Learn more...](/docs/manageapps/depapps.html#appmanifest)
 ```
applications:
- name: bluemix-aspnetcore-starter
  host: aspnetcore-starter
  domain: mybluemix.net
  memory: 512M
  buildpack: https://github.com/cloudfoundry/dotnet-core-buildpack.git
 ```

## 4. Deploy the app

You can use the Cloud Foundry CLI to deploy apps.

To start, login to your Bluemix account:
  ```
cf login
  ```

Choose your API endpoint
  ```
cf api <API-endpoint>
  ```

Replace the *API-endpoint* in the command with an API endpoint from the following list.

|URL                             |Region          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | US South       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |

Be sure you are in the main directory, **aspnet-core-helloworld**, for your application.

Push your application to Bluemix
  ```
cf push
  ```

This can take a minute. If there is an error in the deployment process you can use the command `cf logs <Your-App-Name> --recent` to troubleshoot.

When deployment completes you should see a message indicating that your app is running.  View your app at the URL listed in the output of the push command.  You can also issue the
  ```
cf apps
  ```
  command to view your apps status and see the URL.
