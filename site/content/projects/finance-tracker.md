+++
author = "Deep Mehta"
title = "Finance Tracker"
date = "2021-12-31"
description = "Sample Application to show Angular Web App + ASP.NET Core Web API"
tags = [
    "github",
    "azure",
    "angular",
    "asp.net",
    "authentication"
]
+++

![FeaturedImage](/images/projects/finance_tracker_api.png)

## Introduction

---

The finance tracker is a sample application created to demonstrate how Angular Web App for frontend and ASP.Net Core API for backend can be configured to work together. The cloud architecture for this application is hosted on Azure.

## Financial Tracker BackEnd

---

This api is developed using ASP.NET Core 3.1 and is hosted on Azure App Service.

Following Azure Resources are being utilized:

1. Azure App Service Plan + Azure App Service - Host the API
2. Azure SQL Server + Azure SQL DB - Store data
3. Azure Keyvault - Store Secrets
4. Azure Application Insights - Logging

![Azure Resources](/images/projects/finance_tracker_azure.png)

We followed the DB first approach and performed the following steps:

1. Created a SQL DB project
2. Created a user in SQL DB called gh-runner by running following commands

    ```sql
    CREATE USER [gh-runner] WITH PASSWORD = 'password';
    alter role db_datareader add member [gh-runner];
    alter role db_datawriter add member [gh-runner];
    alter role db_executor add member [gh-runner];
    GRANT VIEW DEFINITION TO [gh-runner];
    GRANT ALTER TO [gh-runner];
    GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [gh-runner];
    GRANT REFERENCES TO [gh-runner];
    ```

3. Using GitHub actions - Build & Deploy the SQL DB
4. Created API Project
5. Using the following command, created models and dbContext: "Scaffold-DbContext "Server=tcp:{server_url},1433;Initial Catalog={db_name};Persist Security Info=False;User ID={user_id};Password={password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models"
6. Gave DB access to Azure App Service API by running following command:

    ```sql
    create user [financetracker-api] from external provider;
    alter role db_datareader add member [financetracker-api];
    alter role db_datawriter add member [financetracker-api];
    alter role db_executor add member [financetracker-api];
    ```

7. Then deployed the azure app service as a docker image to GitHub Container Registry using GitHub actions.

The API project has following features:

1. APIs authenticated with Azure AD
2. Keyvault and SQL accessed by managed identity, thus no secrets exposed anywhere

## Finance Tracker FrontEnd

---

This project is created using Angular and hosted on Azure App Service.

The following steps were performed to develop and configure this app:

1. ng new financial-tracker - Initialize default angular application
2. npm install --force - Install the required modules
3. Generate services and components using ng generate service api, ng generate component AddInvestmentComponent
4. Configure authentication using this article: [Angular App - Azure AD Auth](https://www.c-sharpcorner.com/article/easily-enable-azure-ad-authentication-in-angular-and-web-api-core-app/)
5. Run the application locally: ng serve
6. Create Docker image for angular app, and push it to GitHub container registry using GitHub actions.
7. Configure app service to pull image from this container.

![Frontend UI](/images/projects/finance_tracker_frontend.png)

{{< notice info "Project Artifacts & Details" >}}
**Website:** [Finance Tracker APP](https://financetracker-app.azurewebsites.net/)

**API:** [Finance Tracker API](https://financetracker-api.azurewebsites.net/swagger)

**Repository Frontend:** [https://github.com/deep-mm/FinancialTracker-Frontend](https://github.com/deep-mm/FinancialTracker-Frontend)

**Repository Backend:** [https://github.com/deep-mm/FinanceTracker-Backend](https://github.com/deep-mm/FinanceTracker-Backend)

**Technology:** Azure, Angular, ASP.NET, Azure AD, Database
{{< /notice >}}
