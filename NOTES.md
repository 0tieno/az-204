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

The deployment slot functionality in App Service is a powerful tool that enables you to preview, manage, test, and deploy your different development environments.

> **Note**  
> To make settings swappable, add the app setting `WEBSITE_OVERRIDE_PRESERVE_DEFAULT_STICKY_SLOT_SETTINGS` in every slot of the app and set its value to 0 or false. These settings are either all swappable or not at all. You can't make just some settings swappable and not the others. Managed identities are never swapped and aren't affected by this override app setting.

**Exercise:**  
https://microsoftlearning.github.io/mslearn-azure-developer/instructions/azure-app-service/02-app-service-deployment-slots.html

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

---

# Azure Functions

Azure Functions lets you develop serverless applications on Microsoft Azure. You can write just the code you need for the problem at hand, without worrying about a whole application or the infrastructure to run it.

Azure Functions is a serverless compute service, whereas Azure Logic Apps is a serverless workflow integration platform.  
For most scenarios, it's the best choice.

A function app is composed of one or more individual functions that are managed, deployed, and scaled together.  
Think of a function app as a way to organize and collectively manage your functions.

A Functions project directory contains the following files in the project root folder, regardless of language:
- host.json
- local.settings.json
- Other files in the project depend on your language and specific functions.

The host.json metadata file contains configuration options that affect all functions in a function app instance. Other function app configuration options are managed depending on where the function app runs:

- Deployed to Azure: Configured in your application settings
- On your local computer: Configured in the local.settings.json file.

The local.settings.json file stores app settings, and settings used by local development tools. Settings in the local.settings.json file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

> **Important**  
> Because the local.settings.json might contain secrets, such as connection strings, you should never store it in a remote repository.

**Synchronize settings**  
When you develop your functions locally, any local settings required by your app must also be present in the app settings of the deployed function app. You can also download current settings from the function app to your local project.

A trigger defines how a function is invoked and a function must have exactly one trigger. Triggers have associated data, which is often provided as the payload of the function.

Binding to a function is a way of declaratively connecting another resource to the function; bindings might be connected as input bindings, output bindings, or both. Data from bindings is provided to the function as parameters.

Bindings are optional and a function might have one or multiple input and/or output bindings.

**Exercise:**  
https://microsoftlearning.github.io/mslearn-azure-developer/instructions/azure-functions/01-functions-create-vscode-http.html

---

# Azure Blob Storage

Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

## Types of storage accounts
- Standard
- Premium

The available access tiers are:

- **The Hot access tier**, which is optimized for frequent access of objects in the storage account. The Hot tier has the highest storage costs, but the lowest access costs. New storage accounts are created in the hot tier by default.
- **The Cool access tier**, which is optimized for storing large amounts of data that is infrequently accessed and stored for a minimum of 30 days. The Cool tier has lower storage costs and higher access costs compared to the Hot tier.
- **The Cold access tier**, which is optimized for storing data that is infrequently accessed and stored for a minimum of 90 days. The cold tier has lower storage costs and higher access costs compared to the cool tier.
- **The Archive tier**, which is available only for individual block blobs. The archive tier is optimized for data that can tolerate several hours of retrieval latency and remains in the Archive tier for a minimum 180 days. The archive tier is the most cost-effective option for storing data, but accessing that data is more expensive than accessing data in the hot or cool tiers.

Blob storage offers three types of resources:
- The storage account.
- A container in the storage account
- A blob in a container

Azure Storage supports three types of blobs:
- Block blobs
- Append blobs
- Page blobs

Azure Storage uses service-side encryption (SSE) to automatically encrypt your data when it's persisted to the cloud.  
Azure Storage encryption is enabled for all storage accounts and can't be disabled.

All Azure Storage resources are encrypted, including blobs, disks, files, queues, and tables. All object metadata is also encrypted.

There's no extra cost for Azure Storage encryption.

---

# Azure Cosmos DB

Azure Cosmos DB is a fully managed NoSQL database designed to provide low latency, elastic scalability of throughput, well-defined semantics for data consistency, and high availability.

Azure Cosmos DB offers 99.999% read and write availability for multi-region databases.

Azure Cosmos DB offers five well-defined levels. From strongest to weakest, the levels are:

- Strong
- Bounded staleness
- Session
- Consistent prefix
- Eventual

With Azure Cosmos DB, you pay for the throughput you provision and the storage you consume on an hourly basis.

Change feed in Azure Cosmos DB is a persistent record of changes to a container in the order they occur.

---

# Azure Container Registry & Containers

Azure Container Registry (ACR) is a managed, private Docker registry service based on the open-source Docker Registry 2.0

Use Azure Container Registry Tasks (ACR Tasks) to streamline building, testing, pushing, and deploying images in Azure. Configure build tasks to automate your container OS and framework patching pipeline, and build images automatically when your team commits code to source control.
Dockerfiles typically include the following information:

- The base or parent image we use to create the new image
- Commands to update the base OS and install other software
- Build artifacts to include, such as a developed application
- Services to expose, such a storage and network configuration
- Command to run when the container is launched

---

# Azure Container Instances

Azure Container Instances (ACI) offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.

By default, Azure Container Instances are stateless. If the container crashes or stops, all of its state is lost. To persist state beyond the lifetime of the container, you must mount a volume from an external store.

---

# Azure Container Apps

Azure Container Apps is a serverless container service that supports microservice applications and robust autoscaling capabilities without the overhead of managing complex infrastructure.

Azure Container Apps enables you to run microservices and containerized applications on a serverless platform that runs on top of Azure Kubernetes Service.

In most situations where you want to run multiple containers, such as when implementing a microservice architecture, deploy each service as a separate container app.

Container Apps doesn't support Azure Key Vault integration. Instead, enable managed identity in the container app and use the Key Vault SDK in your app to access secrets.

The Distributed Application Runtime (Dapr) is a set of incrementally adoptable features that simplify the authoring of distributed, microservice-based applications.

---

# Azure Key Vault

Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys.

The Azure Key Vault service supports two types of containers: vaults and managed hardware security module(HSM) pools. Vaults support storing software and HSM-backed keys, secrets, and certificates. Managed HSM pools only support HSM-backed keys.

A common challenge for developers is the management of secrets and credentials used to secure communication between different components making up a solution. Managed identities eliminate the need for developers to manage credentials.

---

# Azure App Configuration

Azure App Configuration provides a service to centrally manage application settings and feature flags.

Use App Configuration to store all the settings for your application and secure their accesses in one place.

---

# Azure API Management

Azure API Management is made up of an API gateway, a management plane, and a developer portal. These components are Azure-hosted and fully managed by default.

---

# Azure Queue Mechanisms

Azure supports two types of queue mechanisms: Service Bus queues and Storage queues.

You can specify two different modes in which Service Bus receives messages: Receive and delete or Peek lock.
