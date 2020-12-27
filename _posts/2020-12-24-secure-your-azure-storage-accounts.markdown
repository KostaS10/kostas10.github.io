---
layout: post
title:  "Secure your Azure Storage Accounts"
date:   2020-12-24 13:12:36 +0200
categories: Azure, Security, Storage Account
---

### What is Azure Storage account?
----------------------------------

\
Azure Storage account is a great service Microsoft provides for storing your data that is accessible from anywhere in the world over HTTP or HTTPS, but if missconfigured, it can mean that your data is exposed to people that should not have the access to it.
Azure Storage account can contain blobs, files, queues, tables and disks and data in your Azure storage account is durable and highly available, secure, and massively scalable.

Because of all of this, we need to make sure that we are following security best practices and we will discuss them further in this post and we will focus specifically on Blob storage.

### Blob storage security considerations
----------------------------------

\
Just to cover the basics for those new to this Azure service, Azure Blob storage is an object storage optimized for storing large amount of unstructured data, examples being text or binary data.
Individual files are referred to as Blobs, and Blobs are contained inside of a Container.

When we create Storage Account and want to store Blobs inside of it, we need to first create a Container where those Blobs will be stored.
Other than name that we have to give to that container, we are presented with a choice of defining public access level on the Container.

<img src="https://infrasecurity.xyz/media/containeraccesslevel.PNG" style="display: block; margin: auto;" />

We will discuss all of these options, and why you may opt for a certain level, depending on your use case.

**Container level**

Setting your Container to Container level means that all container and blob data can be read by anonymous request, meaning that you don't put any restrictions to accessing the files stored there.

In addition, as long as someone has the Storage account name and Container name they can list all of the Blobs located in there.

<img src="https://infrasecurity.xyz/media/blobenum.PNG" style="display: block; margin: auto;" />

Also, direct link to accessing those Blobs is right there, so if we access that URL we see the contents of the Blob.

<img src="https://infrasecurity.xyz/media/publicdocument.PNG" style="display: block; margin: auto;" />

**Blob level**

This Container access level is more restrictive in a way that anonymous requests now cannot list the Blobs in this Container, but if they know the exact name of a Blob in question, they can still see the Blob content. Listing Blobs, however,

 results in an error.

<img src="https://infrasecurity.xyz/media/enumerror.PNG" style="display: block; margin: auto;" />

**Private level**

Setting the Container to this access level means that anonymous access is disallowed and all those requests would result in a same error as before, ResourceNotFound. This access level is set by default regardless of the method you are using to create the Container.

So if anonymous access is forbidden, how would you delegate access to Blobs? Authorizing options for Blobs are:

* Shared Key
* Shared Access Signature
* Azure Active Directory

Shared Key authorization utilizes Access keys that are generated when you create Storage account and the keys grant you access to everything inside it, similar to a root/administrator account.
Microsoft strongly suggests that the keys should not be distributed to others, hard-coded or stored in plane-text.

Shared Access Signatures, also known as SAS, enables you to grant limited access to containers and blobs in your storage account. Using SAS you can specify which resources client has access to, permissions on those resources and for how long.

Azure Active Directory can also be used as an authorization method so you can utilize Role-Based Access Control (RBAC).

### Storage Account network security considerations
----------------------------------

\
By default, Storage Account allowes access from all networks, including the internet. Good things is that Azure provides us with Networking settings when configuring Storage Account so we can restrict access to certain Virtual Networks by changing the access option to **Selected Networks**. There is an option to whitelist public IP addresses and allow them access as well. That can be done from **Firewall** section of the Storage Account.

Some additional exceptions to the firewall and access restrictions can be configured from the **Exceptions** portion of the configuration. All of the settings are shown in the screenshot below.

<img src="https://infrasecurity.xyz/media/storagenetworking.PNG" style="display: block; margin: auto;" />

**Private endpoint connection**

Another security feature that we can utilize to further restrict access to Storage accounts is to use Private endpoint connections.
The private endpoints use an IP address from the Virtual Network in your Azure subscription for your Storage account service, and the data is accessed over a Private Link.

What this all means is that the network traffic between the clients and the Storage account goes over the Virtual Network and a private link on the Microsoft backbone network, thus eliminating the need to go throught the internet. Private endpoints can be easily enabled from the same Networking blade in your Storage account settings.

<img src="https://infrasecurity.xyz/media/privateendpoint.PNG" style="display: block; margin: auto;" />

