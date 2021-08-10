+++
author = "Deep Mehta"
title = "GitHub Action - Set Variables"
date = "2020-11-23"
description = "GitHub Action to use variable groups in GitHub workflows"
tags = [
    "github",
    "actions",
    "devops",
    "marketplace"
]
+++

### Introduction

---

Are you missing the Azure DevOps Library variable groups in GitHub Actions? If yes, then this action will act as a substitution of Library variable groups in GitHub.
This is a GitHub Action used to convert variables.json files into environment variables.

{{< figure src="/images/projects/set_var_github_marketplace.png" link="https://github.com/marketplace/actions/set-variable" alt="Screenshot of set variable action on GitHub Marketplace" >}}

This action contains a bash script which reads a variable.json file in `.github > variables` folder and then add these values as environment variables in workflow, thus allowing one to share variables among multiple workflows.

Find more details about how to use it: [GitHub Marketplace](https://github.com/marketplace/actions/set-variable)

{{< notice info "Project Artifacts & Details" >}}
**Marketplace:** [set-variable](https://github.com/marketplace/actions/set-variable)

**Repository:** [https://github.com/deep-mm/set-variables](https://github.com/deep-mm/set-variables)

**Technology:** GitHub actions, yaml, bash
{{< /notice >}}
