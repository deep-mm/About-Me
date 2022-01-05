+++
author = "Deep Mehta"
title = "QnA - PlugnPlay"
date = "2022-01-05"
description = "This is a reusable IP that can be used to publish your customized QnA bot for free in less than 10 minutes."
tags = [
    "github",
    "azure",
    "bot",
    "cognitive",
    "IP",
    "AI",
    "DevOps"
]
+++

[![FeaturedImage](/images/projects/qna_main.png)](https://yoururl.tech/qnayt)

## Introduction

---

The QnA Maker is intended to behave as a reusable IP that can be used to deploy a **customized QnA Bot Service** onto any Azure subscription for **free**. It just takes about **10 minutes** to have your personalized QnA Bot up and running.

## Project Details

---

This project has 3 parts:

1. Backend where the **QnA Knowledge Base** service is hosted for which we utilize Azure.
2. GitHub Repository FAQ files are utilized to update the QnA service knowledge base automatically.
3. Frontend where you can interact with the QnA service, which in our case in GitHub Issues Bot & Azure Bot Service

The **Architecture** is defined in the diagram below:

![Architecture](/images/projects/qna_architecture.png)

Following Azure Resources are being utilized:

1. Azure Language Service - Store Knowledge Base
2. Azure Search Service - Question and Answer search
3. Azure Bot Service - Frontend for QnA
4. Azure App Service Plan & App Service - Hosting the bot

![Azure Resources](/images/projects/qna_resources.png)

## QnA Backend

---

The Backend language service and knowledge base initialization is automated using ARM templates and powershell scripts. The [QnA-Infra-Deploy](https://github.com/deep-mm/QnA-Service-PlugnPlay/blob/main/.github/workflows/deploy-infra.yml) workflow is responsible for deploying this onto Azure.

The [deploy.json](https://github.com/deep-mm/QnA-Service-PlugnPlay/blob/main/ARM_Template/deploy.json) ARM Template deploys the language service and search service. As an output of this ARM template we get the subscription key to the language service which we store as GitHub secret to be used in other workflows.

The [createLanguageProject.ps1](https://github.com/deep-mm/QnA-Service-PlugnPlay/blob/main/.github/scripts/createLanguageProject.ps1) script is used to initialize the knowledge base with predefined [witty chit-chat](https://qnamakerstore.blob.core.windows.net/qnamakerdata/editorial/english/qna_chitchat_witty.tsv) QnA pairs.

With this, now we have our default QnA service up and running.

Next step is to add customized Question and Answer pairs to this knowledge base. For this we have created a GitHub action [QnA-KB-Deploy](https://github.com/deep-mm/QnA-Service-PlugnPlay/blob/main/.github/workflows/deploy-qna.yml), which is responsible for picking up all the md files within the [FAQs folder](https://github.com/deep-mm/QnA-Service-PlugnPlay/tree/main/FAQs) and automatically deploying all the question answer pairs withing these files to the knowledge base.

These markdown files expect a certain format to be picked up by the automated script.

![FAQ file format](/images/projects/qna_faq_format.png)

The knowledge base can be explored and tested in the [Language Studio](https://language.cognitive.azure.com/).

![Language Studio](/images/projects/qna_lang_studio.png)

## QnA Frontend

---

The frontend here is of 2 different types:

1. [GitHub Issues Bot](https://github.com/deep-mm/QnA-Service-PlugnPlay/issues/1) (Doesn't require any additional infrastructure)
The github workflow [GH-Issue-Bot](https://github.com/deep-mm/QnA-Service-PlugnPlay/blob/main/.github/workflows/gh-issue-bot.yml) continuously listens for issue comments, and if there is a comment starting with @bot, it calls the QnA API and gets the answer and then replies to that issue. The list of language service REST API can be found here [Question Answering APIs](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/questionanswering/question-answering-projects).

    ![GitHub Issue Bot](/images/projects/qna_issue_bot.png)

2. [Azure Bot Service](https://yoururl.tech/bot) (Required infrastructure)
The Azure Bot service is an easy to deploy service and can be used across various channels including Web chat, Microsoft Teams, Twilio etc. In the backend it also does the same task of reaching out to the QnA service and getting back the answers.

    ![Azure Bot Service](/images/projects/qna_azure_bot.png)

## How to use

---

We saw what it is, and I am sure you must be curious as to how you can use this IP to deploy your own QnA bot.
Lets find out!

Following steps needs to be performed in order to deploy this:

1. Download the Release v1 code from here [Download](https://github.com/deep-mm/QnA-Service-PlugnPlay/archive/refs/tags/v1.zip)
2. Create a GitHub repository and upload the downloaded code there.
3. Ensure you have an active azure account and subscription, if not you can create one here: [Create Azure Account for Free](https://azure.microsoft.com/en-in/free/).
> This wont cost you anything, since the services we will be deploying are under the free tier.
4. Add the following secrets in your GitHub repository

    ![GitHub Secrets](/images/projects/qna_secrets.png)

    a. AZURE_CREDENTIALS as explained here: [Azure Login GitHub Action](https://github.com/marketplace/actions/azure-login#configure-a-service-principal-with-a-secret)

    b. PAT - Create a GitHub PAT as explained here: [How to create a GitHub PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with scope as **repo**.

    c. QNANAME - This must be a unique name across azure, to verify you can enter it here: [Name verification](https://portal.azure.com/#create/Microsoft.CognitiveServicesTextAnalyticsWithConfigurations) and verify that it is being accepted.

5. Update the file under `.github > variables > qna.json`. Here update the subscriptionId value to your azure subscription id, and the qnaName value to the qnaName you finalized in **step 4c**.
6. Now run the workflow QnA-Infra-Deploy manually which will deploy the resources onto Azure.
7. Next, go to the folder `FAQs`, and here you can update the markdown files to any question answers you wish to see your bot reply.
8. Now the workflow QnA-KB-Deploy will be triggered and your updated QnA will be deployed to knowledge base.
9. You can go to the [Language Portal](https://language.cognitive.azure.com/) to verify the same.

That's it! We have out service up and running.
To test it out, you can create a new issue in the same repository, and add a comment `@Bot {your question}` and in about 15 seconds you should see the reply coming in!

To deploy the **Azure Bot service**

1. Go to [Language Portal](https://language.cognitive.azure.com/).
2. Open the project with the name you entered in the qnaName variable.
3. Go to `Deploy Knowledge Base`
4. Click on `Create a bot`
5. Now follow the steps and deploy it to the resource group QnA Maker.
6. **[IMPORTANT]** Once deployed, go to the app service plan that it created and click on Scale Up. Here change the pricing tier to F1 to avoid any charges to your account.

That's it! We have our bot up and running.
Simply go to the web app bot resource, and select Test in Web Chat. Now you will be able to test your question answers here.

Thus we saw how easy it is to deploy your customized QnA bot for free. Now that you have the base ready, you can use this to customize as per your requirements.

{{< notice info "Project Artifacts & Details" >}}
**Youtube Video:** [Deploy a Personal QnA Bot for free in less than 10 minutes](https://yoururl.tech/qnayt)

**Azure Bot Service:** [Azure Bot](https://yoururl.tech/bot)

**GitHub Issues Bot:** [GitHub Issue Bot](https://github.com/deep-mm/QnA-Service-PlugnPlay/issues/1)

**Repository** [https://github.com/deep-mm/QnA-Service-PlugnPlay](https://github.com/deep-mm/QnA-Service-PlugnPlay)

**Technology:** Azure, Cognitive, GitHub, DevOps
{{< /notice >}}
