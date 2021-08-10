+++
author = "Deep Mehta"
title = "GitHub Probot App - Deployed on Azure Functions"
date = "2021-08-10"
description = "Example of GitHub Probot App hosted on Azure Functions that listens to issue.open event and performs actions on that issue."
tags = [
    "github",
    "probot",
    "devops",
    "app",
    "automation",
    "azure",
    "functions",
    "node.js"
]
+++

## Introduction

---

[GitHub Apps](https://docs.github.com/en/developers/apps) allow you to automate and improve your workflow. You can make use of almost every GitHub REST API in the GitHub App except for the ones which doesn't have mentioned `Works with GitHub Apps` in [here](https://docs.github.com/en/rest/reference/).

In this blog, we showcase how easy it is to create a GitHub App using [Probot](https://probot.github.io/docs/README/) framework, and in the second part we show how to deploy this App on Azure Functions. Stay Tuned!

{{< notice info >}}
Throughout this demo we will be making use of this repository: [first-app-probot](https://github.com/deep-mm/first-app-probot). Have this open for your reference.
{{< /notice >}}

### Initialize & Run Probot App locally

In this section we will initialize a GitHub App with Probot and see it in action.

---

Initializing a Probot GitHub App requires installed node version to be greater than 10.0.0. You cam check this by using `node -v` command on your desktop. If needed you can always find the latest node version here: [NodeJS](https://nodejs.org/).

1. Follow the steps mentioned in the [Probot Documentation](https://probot.github.io/docs/development/#generating-a-new-app)

   ![Initialize GitHub App with Probot](/images/projects/probot_initialize.png)

2. Once app is initialized, run the app locally by running following command `npm start`
3. Now that the app is running, open this url in the browser [http://localhost:3000/](http://localhost:3000/).

   ![Probot App on LocalHost](/images/projects/probot_app_localhost.png)

4. Click on Register GitHub App, select your GitHub Account and install there.

    ![Probot App on GitHub](/images/projects/probot_app_github.png)

5. Now restart the server in your terminal by `Ctrl + C` > `Y`. Then run `npm start`.
6. Now open any issue in your any of the repository and see an automated comment directly visible in that issue.

    ![Probot App in action](/images/projects/probot_app_local_inaction.png)

7. The GitHub App, most important file where all the logic is mentioned is `index.js`.
8. Let's use the [octokit rest api](https://octokit.github.io/rest.js/v18) to also assign the issue to a user by default whenever it is created. This Octokit Rest API is everything you will need to experiment with GitHub Apps. This will help you automate almost everything.

    ![Octokit REST API](/images/projects/probot_octokit_rest.png)

9. Lets add the following lines to index.js to also support assign feature.

    ```node
    const assignee = context.issue({
      assignees: "{GitHub_Username}",
    });
    context.octokit.issues.addAssignees(assignee);
    ```

10. Once Added, restart the server and see the code in action by creating a new issue.

    ![Probot App in action](/images/projects/probot_app_local_inaction_1.png)

### Deploy GitHub App on Azure Functions

In this section we will see how can we host this Probot App on Azure Functions.

---

1. Create a folder in the main folder called `{Your Function Name}` and add 2 files within it:
   - function.json: Defines the function app - httpTrigger with noauth and supports POST
   - index.js: Defines the initial script of function app - Initialize the Probot App defined in index.js

    The content of these files will remain same irrespective of any app, so you can copy this from the repository mentioned in the **Project Artifacts & Details** section at the end of this page.

2. Update the package.json & package-lock.json exactly the same as mentioned in the first-app-probot repository. This has updated node packages required for the function app.

3. Create a new repository on GitHub and push this code there.

4. Create a [new function App on Azure](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-function-app-portal). Then configure the deployment center to connect the GitHub repository we created in step 3.

5. This will automatically setup the CI/CD in the GitHub Actions and deploy the Function App.

    ![GitHub Actions CI/CD success run](/images/projects/probot_github_cicd.png)

6. Add 3 configuration app settings in azure function app (Values will be found in local .env file):

   - APP_ID
   - PRIVATE_KEY
   - WEBHOOK_SECRET

    ![Updated function app settings](/images/projects/probot_function_appsettings.png)

7. Copy the ProbotFunctionApp Url from Azure Portal. Open the GitHub App settings and change the webhook url now to this function app url. This will ensure that now whenever an issue is opened, a request will be sent to the function app and not to the old local webhook.

    ![GitHub App with updated settings](/images/projects/probot_app_github_update.png)

8. Now, if you open an issue, a request is sent to function app and we can see the issue comment as well as it being assigned.

    ![Azure Function App Monitor](/images/projects/probot_function_monitor.png)

### Demonstration Video

{{< youtube 4EzYLqR_vnU >}}

---

{{< notice info "Project Artifacts & Details" >}}
**Marketplace:** [first-app-probot](https://github.com/apps/first-app-probot)

**Repository (first-app-probot):** [https://github.com/deep-mm/first-app-probot](https://github.com/deep-mm/first-app-probot)

**Repository (GitHub-App-Probot-Example):** [https://github.com/deep-mm/GitHub-App-Probot-Example](https://github.com/deep-mm/GitHub-App-Probot-Example)

**Technology:** GitHub Apps, Azure Functions, Node, DevOps, Probot, Octokit
{{< /notice >}}
