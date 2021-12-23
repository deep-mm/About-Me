+++
author = "Deep Mehta"
title = "Taskgroup in GitHub Workflow"
date = "2021-12-23"
description = "How to develop and use templates in GitHub workflows"
tags = [
    "github",
    "devops",
    "actions"
]
+++

This article will demonstrate how we can make use of **taskgroup/template** in GitHub workflow.

If you are someone coming from Azure DevOps world to GitHub DevOps, you will be curious about templates and variable groups, which act as a basic necessity when creating pipelines for multiple environments. In this article we will see how we can utilize these features in GitHub.

Throughout this article, I will be using this repository: [TaskgroupGitHubWorkflow](https://github.com/deep-mm/TaskgroupGitHubWorkflow), for the demo, so feel free to fork this repository and get your hands dirty.

### Variables

---

Variable groups can be defined and used in GitHub workflows using the following action: [Set-Variables](https://github.com/marketplace/actions/set-variable).
In our demo to develop templates, this action plays a very important role. I will explain in-depth on how we utilize this action, but for now make a note that we have 3 variable groups defined in our `.github > variables` folder. These variable groups are logically divided based on release environments, which are dev,qa,prd.
Thus we have 3 variable groups:

* variable-dev
* variable-qa
* variable-prd

### GitHub Reusable Workflows + GitHub Composite Action

---

[GitHub Composite action](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/) allows one to create a template file containing composite actions. This template file in GitHub is known as a composite action. A composite action takes an input of a variable, and then we can utilize these variables to run same set of actions but in different environments.
For our example, we have created a composite action called [deploy-azure.yml](https://github.com/deep-mm/TaskgroupGitHubWorkflow/blob/main/.github/actions/deploy-azure/action.yml).

This action takes an input of variable environment, which is then utilized in subsequent steps.
This action has 3 composite steps:

1. Echo output
2. Set environment variables - depending on variable input select the variable group
3. Create resource group - depending on variable input deploy the resource group

[GitHub Reusable workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows) helps reduce duplication and increase efficiency and accuracy of workflows. This makes workflows easier to maintain and allows you to create new workflows more quickly by building on the work of others, just as you do with actions. For our example, we have created a reusable workflow called [reusable-template.yml](https://github.com/deep-mm/TaskgroupGitHubWorkflow/blob/main/.github/workflows/reusable-template.yml).
This reusable workflow then calls the composite action with the required input to run multiple steps in that particular environment.

Then this reusable workflow is utilized in our main workflow [Template-Action-Composite](https://github.com/deep-mm/TaskgroupGitHubWorkflow/blob/main/.github/workflows/template-new.yml), in all three jobs release-dev, release-qa & release-prd. The only change being in the input provided to the reusable workflows.

The output here looks something like this:
![GitHub Taskgroup Output](/images/blogs/github_taskgroup_output.png)

The relation between main workflow, reusable workflow, and composite action is as follows:

**Main Workflows** *1------n* **Reusable Workflows** *1------n* **Composite Actions**

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
