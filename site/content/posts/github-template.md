+++
author = "Deep Mehta"
title = "Taskgroup in GitHub Workflow"
date = "2021-09-02"
description = "How to develop and use templates in GitHub workflows"
tags = [
    "github",
    "devops",
    "actions"
]
+++

This article will demonstrate how we can make use of **taskgroup/template** in GitHub workflow.

If you are someone coming from Azure DevOps world to GitHub DevOps tools, 2 major things you would be missing are variable groups and templates. I will demonstrate how we can get these two features in GitHub by utilizing actions available in GitHub marketplace.

There are 2 ways to achieve this:

1. GitHub Composite Action
2. Running same workflow multiple times

We will look at both of these methods in the article below.

Throughout this article, I will be using this repository: [TaskgroupGitHubWorkflow](https://github.com/deep-mm/TaskgroupGitHubWorkflow), for the demo, so feel free to fork this repository and get your hands dirty.

### Variables

---

Variable groups can be defined and used in GitHub workflows using the following action: [Set-Variables](https://github.com/marketplace/actions/set-variable).
In our demo to develop templates, this action plays a very important role. I will explain in-depth on how we utilize this action, but for now make a note that we have 3 variable groups defined in our `.github > variables` folder. These variable groups are logically divided based on release environments, which are dev,qa,prd.
Thus we have 3 variable groups:

* variable-dev
* variable-qa
* variable-prd

### 1. GitHub Composite Action

---

[GitHub Composite action](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/) allows one to create a template file containing composite actions. This template file in GitHub is known as a composite action. A composite action takes an input of a variable, and then we can utilize these variables to run same set of actions but in different environments.
For our example, we have created a composite action called [deploy-azure](https://github.com/deep-mm/TaskgroupGitHubWorkflow/blob/main/.github/actions/deploy-azure/action.yml).

This action takes an input of variable environment, which is then utilized in subsequent steps.
This action has 3 composite steps:

1. Echo output
2. Set environment variables - depending on variable input select the variable group
3. Create resource group - depending on variable input deploy the resource group

Then this composite action is utilized in our main workflow [Template-Action-Composite](https://github.com/deep-mm/TaskgroupGitHubWorkflow/blob/main/.github/workflows/template-new.yml), in all three jobs release_dev, release_qa & release_prd. The only change being in the input provided to the composite action.

The output here looks something like this:
![GitHub Taskgroup Output](/images/blogs/github_taskgroup_output.png)

### 2. Run single workflow multiple times

---

Now, lets go directly to our template workflow file. Here there are 2 important things we need to notice, firstly the workflow has a **trigger** workflow_dispatch with an input of environment value (dev,qa,prd), and secondly we make use of this **action** [Workflow Dispatch](https://github.com/marketplace/actions/workflow-dispatch) at the end of workflow.

Now let me explain you with a diagram how this workflow is a template and how this same workflow can be utilized to deploy to dev,qa,prd environments.

![Template Workflow Explanation](/images/blogs/template-workflow-explanation.png)

When you initiate the workflow in Dev environment, at the end of the workflow, we have a stage called as **Release_To_Next_Env**. This stage checks the current environment, and based on it makes decision on next environment to release the workflow. For e.g. if workflow runs success in dev, it will then run the same workflow using the workflow-dispatch action, but this time the only change being, it will send the input variable as qa, so now the workflow will use the variable group `variable-qa`, and thus this workflow will release to QA, and similarly next run to PRD.

![Template Workflow Run](/images/blogs/template-workflow-run.png)

### Protection Rules

---

This also allows you to have **protection rules** set for your environments, so in this case we have set protection rule for prd environment. Thus whenever the workflow is triggered in prd, it wont run unless its approved by required reviewers.

![Template Workflow Environment](/images/blogs/template-workflow-env.png)

### Azure Resources

---

This is how the resources deployed on Azure look:

![Azure Resources](/images/blogs/template-workflow-resources.png)

---

{{< notice info "Project Artifacts & Details" >}}
**Repository:** [https://github.com/deep-mm/TaskgroupGitHubWorkflow](https://github.com/deep-mm/TaskgroupGitHubWorkflow)

**Technology:** GitHub Actions
{{< /notice >}}
