# Azure App Service Notes

## Overview

Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends.

## Features

- Built-in auto scale support  
- Container support  
- Continuous integration/deployment support  

Continuous integration and deployment for containerized web apps is also supported using either Azure Container Registry or Docker Hub.

- Deployment slots  
- App Service on Linux  

### App Service Environment

App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for running App Service apps. It offers improved security at high scale.

---

## App Service Plan

An App Service plan defines a set of compute resources for a web app to run. One or more apps can be configured to run on the same computing resources (or in the same App Service plan).

**Pricing tier of an App Service plan:**
- **Shared compute:** Free and Shared  
- **Dedicated compute:** The Basic, Standard, Premium, PremiumV2, and PremiumV3  
- **Isolated:** The Isolated and IsolatedV2  

---

## Deployment

### Deploy to App Service

App Service supports both automated and manual deployment.

#### Use deployment slots  
Whenever possible, use deployment slots when deploying a new production build.

If your project designates branches for testing, QA, and staging, then each of those branches should be continuously deployed to a staging slot. This allows your stakeholders to easily assess and test the deployed branch.

---

## Networking

### App Service networking features

By default, apps hosted in App Service are accessible directly through the internet and can reach only internet-hosted endpoints. For many applications, you need to control the inbound and outbound network traffic.

To find the outbound IP addresses currently used by your app in the Azure portal, select Properties in your app's left-hand navigation.

---

## Command-Line Deployment

The `az webapp up` command makes it easy to create and update web apps. When executed, it performs the following actions:

- Create a default resource group if one isn't specified.
- Create a default app service plan.
- Create an app with the specified name.
- Zip deploy files from the current working directory to the web app.

### Outbound networking features:
- Hybrid Connections  
- Gateway-required virtual network integration  
- Virtual network integration  

---

## Scaling

Autoscaling performs scaling in and out, as opposed to scaling up and down.

By default, an App Service Plan only implements manual scaling. 
