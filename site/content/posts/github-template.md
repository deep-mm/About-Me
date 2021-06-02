+++
author = "Deep Mehta"
title = "Taskgroup in GitHub Workflow"
date = "2021-06-02"
description = "How to develop and use templates in GitHub workflows"
tags = [
    "github",
    "devops",
    "actions"
]
+++

This article will demonstrate how we can make use of **taskgroups** in GitHub workflow, a feature which is not currently available out of box in GitHub.

If you are someone coming from Azure DevOps world to GitHub DevOps tools, 2 major things you would be missing are variable groups and templates. I will demonstrate how we can get these two features in GitHub by utilizing actions available in GitHub marketplace.

Throughout this article, I will be using this repository: [TaskgroupGitHubWorkflow](https://github.com/deep-mm/TaskgroupGitHubWorkflow), for the demo, so feel free to fork this repository and get your hands dirty.

### Variables

---

Variable groups can be defined and used in GitHub workflows using the following action: [Set-Variables](https://github.com/marketplace/actions/set-variable).
In our demo to develop templates, this action plays a very important role. I will explain in-depth on how we utilize this action, but for now make a note that we have 3 variable groups defined in our `.github > variables` folder. These variable groups are logically divided based on release environments, which are dev,qa,prd.
Thus we have 3 variable groups:

* variable-dev
* variable-qa
* variable-prd

### Taskgroup/Template

---

Now, lets go directly to our template workflow file. Here there are 2 important things we need to notice, firstly the workflow has a **trigger** workflow_dispatch with an input of environment value (dev,qa,prd), and secondly we make use of this **action** [Workflow Dispatch](https://github.com/marketplace/actions/workflow-dispatch) at the end of workflow.

Now let me explain you with a diagram how this workflow is a template and how this same workflow can be utilized to deploy to dev,qa,prd environments.

![Template Workflow Explanation](/images/blogs/template-workflow-explanation.png)

When you initiate the workflow in Dev environment, at the end of the workflow, we have a stage called as **Release_To_Next_Env**. This stage checks the current environment, and based on it makes decision on next environment to release the workflow. For e.g. if workflow runs success in dev, it will then run the same workflow using the workflow-dispatch action, but this time the only change being, it will send the input variable as qa, so now the workflow will use the variable group `variable-qa`, and thus this workflow will release to QA, and similarly next run to PRD.

![Template Workflow Run](/images/blogs/template-workflow-run.png)

This also allows you to have **protection rules** set for your environments, so in this case we have set protection rule for prd environment. Thus whenever the workflow is triggered in prd, it wont run unless its approved by required reviewers.

![Template Workflow Environment](/images/blogs/template-workflow-env.png)

This is how the resources deployed on Azure look:

![Azure Resources](/images/blogs/template-workflow-resources.png)

{{< notice info "Project Artifacts & Details" >}}
**Repository:** [https://github.com/deep-mm/TaskgroupGitHubWorkflow](https://github.com/deep-mm/TaskgroupGitHubWorkflow)

**Technology:** GitHub Actions
{{< /notice >}}