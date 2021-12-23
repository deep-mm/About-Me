+++
author = "Deep Mehta"
title = "URL Shortener - yourURL"
date = "2021-12-23"
description = "Simple & Easy to use URL Shortner"
tags = [
    "github",
    "azure",
    "function",
    "storage",
    "url",
    "shortcuts"
]
+++

![FeaturedImage](/images/projects/url-shortner-main.png)

## Introduction

---

The URL Shortener is used to shorten and share URLs easily. The cloud architecture for this application is hosted on Azure.

## URL Shortener BackEnd

---

The backend is hosted on Azure and contains following resources:

1. **Function App (url-shortner-aka)** - This hosts all the APIs. The function app post api to add new URLs is protected by function access code.
2. **Storage (urlshortneraka)** - This is utilized by the azure function app to utilize the storage tables to store the urls.

![Azure Resources](/images/projects/url-shortner-azure.png)

## URL Shortener FrontEnd

---

The URL Shortener doesn't have a dedicated frontend, but instead is mainly accessible by 2 APIs:

1. **GET** https://yoururl.tech/{encoded URL} - **UnAuthenticated** - This URL when called, decodes the encoded URL and redirects the user to the actual URL.
2. **POST** https://yoururl.tech/addUrl - **Authenticated** - This URL when called adds the encoded & decoded url pair onto the Azure storage.

But, using the POST Api in day to day basis is not very accessible for end user.
Thus I decided to go with **IPhone Shortcuts**. I created 2 shortcuts for this purpose, one to add url pairs, and other to retrieve and open webpage.

![iPhone Shortcuts](/images/projects/url-shorten-shortcuts.png)

{{< notice info "Project Artifacts & Details" >}}
**Website:** [yourURL](https://www.yoururl.tech)

**Repository:** [https://github.com/deep-mm/URL-Shortner](https://github.com/deep-mm/URL-Shortner)

**Technology:** Azure Functions, Azure Storage, iPhone Shortcuts
{{< /notice >}}
