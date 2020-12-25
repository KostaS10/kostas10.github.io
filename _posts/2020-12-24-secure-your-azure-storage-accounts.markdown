---
layout: post
title:  "Secure your Azure Storage Accounts"
date:   2020-12-24 13:12:36 +0200
categories: Azure, Security, Storage Account
---

### What is Azure Storage account?

Azure Storage account is a great service Microsoft provides for storing your data that is accessible from anywhere in the world over HTTP or HTTPS, but if missconfigured, it can mean that your data is exposed to people that should not have the access to it.
It can contain blobs, files, queues, tables and disks and data your Azure storage account is durable and highly available, secure, and massively scalable.

Because of all of this, we need to make sure that we are following security best practices and we will discuss them further in this post and we will focus specifically on Blob storage.

### Blob storage security considerations

Just to cover the basics for those new to this Azure service, Azure Blob storage is an object storage optimized for storing large amount of unstructured data, examples being text or binary data.
Individual files are referred to as Blobs, and Blobs are contained inside of a Container.

When we create Storage Account and want to store Blobs inside of it, we need to first create a Container where those Blobs will be stored.
Other than name that we have to give to that container, we are presented with a choice of defining public access level on the Container.

<img src="https://infrasecurity.xyz/media/containeraccesslevel.PNG" style="display: block; margin: auto;" />

We will discuss all of these options, and why you may opt for a certain level, depending on your use case.

** Container level **

Setting your Container to Container level means that all container and blob data can be read by anonymous request, meaning that you don't put any restrictions to accessing the files stored there.

In addition, as long as someone has the Storage account name and Container name they can list all of the Blobs located in there.

<img src="https://infrasecurity.xyz/media/blobenum.PNG" style="display: block; margin: auto;" />

Also, direct link to accessing those Blobs is right there, so if we access that URL we see the contents of the Blob.

<img src="https://infrasecurity.xyz/media/publicdocument.PNG" style="display: block; margin: auto;" />

** Blob level **

This Container access level is more restrictive in a way that anonymous requests now cannot list the Blobs in this Container, but if they know the exact name of a Blob in question, they can still see the Blob content. Listing Blobs results in an error.

<img src="https://infrasecurity.xyz/media/enumerror.PNG" style="display: block; margin: auto;" />
