+++
author = "Deep Mehta"
title = "Password Manager"
date = "2021-08-17"
description = "Secure password manager hosted on Azure."
tags = [
    "github",
    "azure",
    "function",
    "keyvault",
    "blazor",
    "password",
    "azuread"
]
+++

![FeaturedImage](/images/projects/pass_main_screen.png)

## Introduction

---

The Password Manager is used to store secrets securely. The cloud architecture for this application is hosted on Azure.

## Password Manager FrontEnd

---

The password manager frontend is developed using Blazor and hosted on Azure App Service. This application is Azure AD protected, and ensures the secrets requested can only be accessed by authorized personnel.

This application allows to:

- View Secrets
- Add Secrets
- Delete Secrets
- Update Secrets

![Show Secrets Screen](/images/projects/pass_second_screen.png)
![Add Secrets Screen](/images/projects/pass_third_screen.png)

**The security part is ensured by 2 factors:**

1. Azure AD authentication
2. A master key is required to access the backend api, only if that is available all the secrets can be accessed or updated.

## Password Manager BackEnd

---

The backend is hosted on Azure and the architecture is:
![Backend Architecture](/images/projects/pass_backend_1.png)

The backend contains following resources:
1. **KeyVault (PasswordManagerVault)** - This stores all the secrets for the password manager, and also the encyrption key. This has network restrictions in place which only allows for vNet addresses to access the Keyvault. Along with this, it has Access Policies in place to ensure only the function app is able to access the keyvault secrets and keys.
2. **Function App (passwordmanagerfn)** - This hosts all the APIs. This is also network restricted within the subnets of the Virtual Network, so it is inaccessible from any other IP. Along with this, the function app is also protected by Azure AD, so for one to access the APIs they must have the function code + valid access token.
3. **App Service Plan (passwordmanagerfn)** - This is the app service plan on which the function app is hosted.
4. **Application Insights (passwordmanagerfn)** - This is where all the function app logs are recorded and can be used for analysis and request tracing.
5. **Storage (passwordmanagerfn)** - This is utilized by the azure function app.
6. **Virtual Network (PasswordManagerVNet)** - This helps to secure resources, ensuring they are only accessible within the VNet, and not from amy other IP.
7. **API Management (PasswordManagerVNet)** - This is used to expose the APIs to external applications, while ensuring security. For someone to access these APIs, along with the APIM subscription key, they will also need to pass the Azure AD access token.

![Azure Resources](/images/projects/pass_backend_2.png)

**Security Overview:**

1. API can only be accessed via APIM
2. To access API, one needs APIM subscription key + Azure AD account
3. Function App API are inaccessible to external applications because of the VNet
4. Keyvault is inaccessible to anyone except function app because of the VNet + Access Policy
5. The secrets sent over the API are encrypted and can be decrytped only by the end application, thus there is no risk of security credentials leak over API calls.

{{< notice info "Project Artifacts & Details" >}}
**Website:** [Password Manager](https://thepasswordmanager.in/)

**Repository (FrontEnd):** [https://github.com/deep-mm/PasswordManager-FrontEnd](https://github.com/deep-mm/PasswordManager-FrontEnd)

**Repository (BackEnd):** [https://github.com/deep-mm/PasswordManager-Backend](https://github.com/deep-mm/PasswordManager-Backend)

**Technology:** Azure Functions, Azure VNet, Azure KeyVault, Blazor, Azure AD
{{< /notice >}}
