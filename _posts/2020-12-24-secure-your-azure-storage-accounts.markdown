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

![Container access levels](https://raw.github.com/KostaS10/kostas10.github.io/blob/master/_posts/containeraccesslevel.PNG)