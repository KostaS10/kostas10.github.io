---
layout: post
title:  "Scan Azure Container Registry images"
date:   2021-01-22 13:12:36 +0200
categories: Azure, Security, Container Registry
---

### What is Azure Container Registry?
----------------------------------

\
Containerization has been a top topic for quite some time, with Docker being the industry favourite.

Azure provides a service called Azure Container Registry which is a managed, private Docker registry service. It allows you to store Docker images which you can use for deploying Docker containers, for example using Azure Container Instances (ACI) or through Azure managed Kubernetes service (AKS).

<br>

### Azure Defender for Container Registries
----------------------------------

\
As a security of our infrastructure is something that all organizations must strive to achieve, it is of great importance that we are able to verify that our images that we are hosting in Container Registry are up-to-date, that there are no known vulnerabilities associated with them.

Microsoft providers us with a way to get an easy win in this domain with Azure Security Center (ASC) and it's offering called Azure Defender for Container Registries. Azure Defender for Container Registries can be enabled by switching to a paid version of Azure Security Center, setting Azure Defender ON, as shown in the screenshot below.

<img src="https://infrasecurity.xyz/media/ascdefender.PNG" style="display: block; margin: auto;" />

You also need to be sure that Container Registry option is turned on so you can start using it.

<img src="https://infrasecurity.xyz/media/ascdefender2.PNG" style="display: block; margin: auto;" />

<br>

### Vulnerability assessment in practice
----------------------------------

\
Now that we have Azure Defender for Container Registries enabled