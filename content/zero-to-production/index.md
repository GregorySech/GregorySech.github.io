+++
title = "Re-learning what it means to make software: Zero to Production in Rust"
date = 2024-05-27
draft = true
[taxonomies]
tags = ["Rust", "Software-Engineering", "Backend", "Book"]
+++

# Post notes.
In March of 2024 I started to read my copy of Zero to Production in Rust by Luca Palmieri. This article is about my experience with it. It might get somewhat technical in some points but it is not meant to be an overall technical read.

Why this book? I am learning Rust, I like the language, I wanted to make a project with it but I didn't want to start with some idea of my own. I feel like I need to be more educated about backend development for when I will implement my own next projects.

When? I work on side project during lunch breaks, on my train commutes or when I wait for some computation to finish. It took me almost 3 months to finish this book/project. It has been worth it.



# Chapter notes
## CH 2
- Consider using a single staged CI instead of 4. Concerned about Github Action billing.
- Problem-based Learning.
  - Makes the book relevant for Rust but for different stacks too.
- User stories to capture requirements!
  - Working in iterations by starting to fulfill *most* of the requirements of all stories at first release. 
    - Then iterate to cover more and more requirements.
    - Iterate on product features, not engineering quality!

## CH 3 - The `/subscriptions` end-point.
- actix-web

- health_check to get familiar with the web framework.
  - The idea is that it's a basic/easy endpoint to start with so it will do a gradual introduction to the technology.
- Refining the requirement
  - "As a blog visitor,
     I want to subscribe to the newsletter,
     So that I can receive email updates when new content is published on the blog."

## CH 5 - Deployment
I want to learn Azure platform for Cloud Computing. So I will use [Azure App Service](https://azure.microsoft.com/en-us/products/app-service) instead of Digital Ocean's.

I started from the optimized container for the application using "cargo-chef".

I am following the ["Deploy and run a containerized web app with Azure App Service"](https://learn.microsoft.com/en-us/training/modules/deploy-run-container-app-service/) module.

Idea abandoned, will come back later.

### Build and store images by using Azure Container Registry
1. Login to azure cli
2. Created the Resource Group using the Azure Portal. But should be equivalent to `az group create --name zero2prod-rg --location westeu`
3. Created the Container Registry `az acr create --name zero2prod --resource-group zero2prod-rg --sku standard --admin-enabled true
`.  
4. Logged into the Container Registry.
5. Build the container using the Container Registry `az acr build --registry zero2prod --image zero2prod .` wait forever.
6. Build the container using Docker `docker build --tag zero2prod --file Dockerfile .`
7. `docker tag zero2prod zero2prod.azurecr.io/zero2prod` no idea why this is necessary.
8. `docker push zero2prod.azurecr.io/zero2prod`
9. Enabling 