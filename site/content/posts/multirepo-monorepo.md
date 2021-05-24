+++
author = "Deep Mehta"
title = "Multi-repo vs Mono-repo"
date = "2021-05-12"
description = "Comparison between multi repo and mono repo"
tags = [
    "repository",
    "structure"
]
+++

I was recently reading  a post about how Google uses the mono-repo approach and has a centralized repository for all its services. This got me thinking  as to what is a better approach, mono-repo or multi-repo?

So, I went back and researched  a bit more into this and pulled out pros and cons of using either of approaches.

### What is Mono-repo?

In a mono-repo approach, all services and codebase are kept in a single repository. Mono-repo doesn't mean a monolithic application but can contains multiple dependent/independent services.

**Pros:**

- Easy on-boarding of new employees
- Fostering collaboration and communication among developers
- Simplify dependency management

**Cons:**

- Performance - With the increasing repository size,the entire process from cloning to push gets degraded
- Continuous Integration & Deployment setup becomes complicated

### What is Multi-repo?

Multi-repo is a way of organizing your services into separate repositories based on logical boundaries like type or use of services.

**Pros:**

- Each service can be versioned separately
- Separate repositories based on areas of responsibilities

**Cons:**

- Difficult to keep track  of dependencies globally across repositories
- Code and Dependency duplication possible
- Enforcing patterns and best practices is hard

This picture accurately depicts the difference between Multi & Mono Repo structure:

![Multi-repo and Monorepo comparison](/images/projects/multirepo-monorepo.png)

> It's essential to bear in mind that going multi-repo comes with trade-offs, as Adam Jacob says in this blog post: "The default behavior of a multi-repo is isolation, and the default behavior of a monorepo is shared responsibility and visibility." Do read this interesting blog: https://medium.com/@adamhjk/monorepo-please-do-3657e08a4b70

To conclude,

Based on my findings, in my opinion each of these approaches have its advantages, but I don’t think I have a definite answer on which structure should we prefer over another, but this decision will vary based on the situation, company, project and product.