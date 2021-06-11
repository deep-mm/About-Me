+++
author = "Deep Mehta"
title = "Library Management System"
date = "2019-08-01"
description = "Library management system to showcase how various azure services can be integrated with a ASP.NET application."
tags = [
    "c#",
    "azure",
    "asp.net",
    "demo"
]
+++

### Introduction

---

This is a library management system which demonstrates how various Azure Cloud Services can be integrated into a .NET Core application.

This project contains 2 major sections we built using ASP.NET C#:

1. Backend-APIs: [https://librarysystem-api.azurewebsites.net/swagger](https://librarysystem-api.azurewebsites.net/swagger)
    ![LMS API](/images/projects/lms_api.png)
2. Frontend Website: [https://librarysystem-mvc.azurewebsites.net](https://librarysystem-mvc.azurewebsites.net)
    ![LMS Website](/images/projects/lms_website.png)

### Azure Services

---

Various Azure Services which are integrated with this application:

1. Azure Keyvault - store all the secrets consumed by the application to avoid any secrets getting compromised.
2. Azure App Service - host the APIs and the frontend website.
3. Azure Search - implement search capabilities in the website.
4. Azure SQL Server - host the sql database
5. Azure SQL Database - store sructured data
6. Azure Reddis Cache - reduce database transactions and increase efficiency
7. Azure Application Insights - store application logs
8. Azure Cosmos DB - store unstructured data
9. Azure Storage Account - store images
10. Azure Active Directory - enable authentication

![LMS Azure Services](/images/projects/lms_azure.png)

{{< notice info "Project Artifacts & Details" >}}
**Website:** [Library Management System](https://librarysystem-mvc.azurewebsites.net/Home)

**Repository:** [https://github.com/deep-mm/LibraryManagementSystem](https://github.com/deep-mm/LibraryManagementSystem)

**Technology:** Azure, ASP.NET, C#
{{< /notice >}}