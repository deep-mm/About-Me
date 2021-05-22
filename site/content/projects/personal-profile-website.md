+++
author = "Deep Mehta"
title = "Personal Profile Website"
date = "2021-05-18"
description = "Personal profile website developed using Azure Static Web, Hugo & GitHub"
tags = [
    "website",
    "profile",
    "hugo",
    "azure",
    "github",
    "devops"
]
+++

### Introduction

---

This project is a personal profile static website created with the help of [Hugo](https://gohugo.io) static site generator, using [hugo-coder](https://themes.gohugo.io/hugo-coder/) theme.

{{< figure src="/images/frontpage.png" link="https://deepmehta.co.in" alt="Screenshot of front page of website" >}}

### DevOps Setup

---

**Continuous Integration & Deployment** is setup in GitHub to deploy the website as and when new updates are pushed. When a new PR is raised against the main branch, the changes are first deployed to a staging environment to verify the changes. The GitHub action sends a notification in the PR tab about the staging site URL on which it is deployed.
Once these changes are verified, the PR can be approved and pushed, and the website is then shifted to production slot.

{{< figure src="/images/projects/github_pr_ss.png" link="https://github.com/deep-mm/About-Me/pull/13" alt="Screenshot of GitHub Pull Request" >}}

### Azure Static Web App

---

[Azure static web app](https://azure.microsoft.com/en-in/services/app-service/static/) is a service provided by Azure to host static website. It also allows to add a custom domain, thus I added the domain `deepmehta.co.in` and thus got my site hosted on my domain.

{{< notice info "Project Artifacts & Details" >}}
**Website:** [deepmehta.co.in](https://deepmehta.co.in)

**Repository:** [https://github.com/deep-mm/About-Me](https://github.com/deep-mm/About-Me)

**Technology:** Azure Static Web App, Azure Custom Domain, Hugo static site generator, GitHub Actions
{{< /notice >}}
