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

You also need to be sure that Container Registry option is turned on so you can start using Azure Defender for Container Registries.

<img src="https://infrasecurity.xyz/media/ascdefender2.PNG" style="display: block; margin: auto;" />

<br>

### Pushing images to ACR
----------------------------------

\
Now that we have Azure Defender for Container Registries enabled, we can start assessing our container images. Image scans are triggered on every push or import, and if the image has been pulled within the last 30 days. When the scan completes, we can see the results in Azure Security Center recommendations.

To show this in practice, let's show an example where we have pushed one Docker image from Docker Hub to our Container Registry. Image in question is named *Damn Vulnerable Web App*, that is usually used for practicing exploits and introducing engineers to ways you can exploit vulnerable applications. You can find the image in the link below:

<a href="https://hub.docker.com/r/vulnerables/web-dvwa">https://hub.docker.com/r/vulnerables/web-dvwa</a>

I've created an Azure Container Registry (ACR) named *kostaacr* beforehand, and here are the few steps that we should do before actually pushing image to ACR:

* Login to Docker Registry
* Pull Docker image from Docker Hub
* Tag image with ACR name so we can push it to ACR
* Push image to our ACR

<img src="https://infrasecurity.xyz/media/acr1.PNG" style="display: block; margin: auto;" />

To verify that the image has been pushed to our ACR, we can check Azure Portal and see that the image is there.

<img src="https://infrasecurity.xyz/media/acr2.PNG" style="display: block; margin: auto;" />

<br>

### Vulnerability assessment in practice
----------------------------------

\
Since the image is now in our ACR, Azure Security Center will scan it and if it finds some vulnerabilities we can see it's findings in the Recommendation section in ASC.

<img src="https://infrasecurity.xyz/media/asc1.PNG" style="display: block; margin: auto;" />

Clicking on the recommendations will open up a new blade where you can see more in detail Azure Container Registries in question, number of vulnerabilities and those vulnerabilities sorted by severity.

<img src="https://infrasecurity.xyz/media/asc2.PNG" style="display: block; margin: auto;" />

All found vulnerabilities are presented in a list and by clicking on each vulnerability provides an option to drill more into each of those vulnerabilities along with:

* Short description of vulnerability
* Additional information about the vulnerability such as CVE number, CVSS score, Severity and if vulnerability is patchable
* Remediation steps so we can fix if fix is available
* Information about specific image in our registry that is affected by the vulnerability

<img src="https://infrasecurity.xyz/media/asc3.PNG" style="display: block; margin: auto;" />

<br>

### Final thoughts
----------------------------------

\
With container technology being on the rise and companies from all different industries are starting to adopt it massively, engineering teams need a way to host their container images with ease while also being able to ensure that the registries that are hosting those images are following security standards and best practices.

Azure Container Registry fills that role perfectly, and also offering security controls in terms of encryption, content trust and network access restrictions.

Azure Security Center and Azure Defender for Container Registry are a great way to integrate vulnerability scanning with your container registry images to make sure all images are without any potential critical vulnerabilities and if any issues arise, you can be notified easily through the ASC.
