+++
author = "Deep Mehta"
title = "Good repo - open source"
date = "2022-10-11"
description = "What is a good open-source repository and why is it important?"
tags = [
 "GitHub",
 "open-source",
 "repository",
 "badges"
]
featuredImage = "/images/blogs/open_source.jpg"
+++

*Open source is about collaborating; not competing*

Say you have an awesome idea and you have the MVP in place and people love it. What's next?
It's used extensively as a product but there's one problem, the open-source community isn't contributing to improving the product and fixing issues.
It's difficult to maintain the product individually and going open source was the next ideal step, so what went wrong?

Maybe the community doesn't have the time to work on it, but that's not in your control. Let's look at the things we can do to ensure contributors feel welcome and motivated to continuously update and improvise the product.

We need a good open-source repo, let's see below what are the components of a good open-source repository and why you should include that in your repository.

I will refer to the following open source repository: [URL-Shortner](https://github.com/CSC510-Group-5/URL-Shortner) as an example of an ideal open source repository throughout this post. Feel free to fork and explore the repository and even contribute to it, if you feel like it!

Let's get started!

## README

This is the most important section of your repository. This is the first thing any contributor checks out and you have less than a minute to convince them that they are welcome to contribute and it's super easy to do so.

Each folder of the repository must define a README that provides an overview of the files that exist within that particular folder, mainly 2 parts, **What** are they and **Why** they are present in that particular folder.

The [main README](https://github.com/CSC510-Group-5/URL-Shortner/blob/main/README.md) must have the following sections:

1. Badges defining various aspects of the repository. We will discuss more badges in the later sections of this post.
2. Why is there a need for this product and what motivation behind this? This section means a lot to both the user of the system as well as the contributor of the system. This may also contain a short video or animation that mentions the problem statement and the motivation.
3. How to use it? This section is mainly utilized by the users of the system to get a head start and understand how they can utilize the system, saving them the time to figure out the system on their own. This should explain the various screens or commands that the users can visit/run and use the product.
4. What? This section can be excluded from the main README and instead put in a different folder (Eg. Architecture). This mainly defines the system architecture, database designs, user flows, and so on. This is not utilized by the end users but is of utmost importance to the contributor of the system because only after they understand the design they can work on fixing or adding new features.

## LICENSE

The repository should clearly define the open-source license it abides by. This helps the contributors of the product to know their rights.

Selecting the right license may seem like a boring task but it's the most important task for an open-source repository. Having a more restrictive license may demotivate contributors or having a more lucrative license may not be the right choice for your product. You can find a list of all available open-source licenses [here](https://choosealicense.com/licenses/) that explain when to select which license.

## Contributing Guidelines

After README, the next page any contributor expects to visit is the CONTRIBUTING.md page which defines the guidelines that the contributors must abide by when raising pull requests to merge their suggested changes.

These guidelines list down what the contributors can do and how.

## Code of Conduct

While having an open forum for people around the world to discuss and share ideas is a wonderful thing there are always some people out there who try to disrespect others. To solve this problem, a code of conduct is required that clearly defines the boundaries and guidelines that all users must follow to keep the repository a safe place to speak up and share thoughts.

The admins of the repository are responsible for banning contributors that don't abide by these guidelines.

## Citation

The Citation file lists down the contributors of the repository that one can utilize when adding this repository as a citation in any research paper where it has been referenced. This ensures that the repository has been cited correctly and all the contributors are rightfully given credit.

## Issues

An open-source repository should make use of GitHub issues efficiently to ensure an easy flow of data from users. What do we mean by the flow of data?
Say a user finds something that needs to be fixed, what should they do? How can that data be known to all users and doesn't get overlooked? How can the contributors know the project timeline of what things are expected to be implemented in the coming months and how can they contribute? How can someone suggest new features and lead discussions on what others think?

All of the above questions have one-word answers i.e. **Issues**.

Issues should be used for everything with correct labels like a bug, feature, release tag, etc. Labels help identify issues from the list and also filter them based on what the user wants to see.

Define an [issue template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) to keep your issues consistent irrespective of who raises them.

## Automations

How do you ensure the changes being added by outside collaborators don't break the existing code? How can you ensure the code follows the style guide at all times? How can you ensure appropriate unit tests have been added by users when adding new code? How can you ensure the changes pushed and merged are also deployed?

While all of the above things can be done manually, you can never be 100% sure, and also it's not very efficient since it would take much more time before a PR is merged with the main code.

Thus, we should ideally have the following automation in place:

1. Automatic style checkers on every PR
2. Automatic unit tests run on every PR
3. Automatic code coverage check on every PR
4. Automatic security checks on every PR
5. Automatic build on every PR

Only if the above automation return success we can be sure that the new code is probably good and can be merged.

> Note: This doesn't mean manual reviewers must not exist in the system. There should always be manual reviewers to ensure that the code being added is needed and if it adds value to the product. Automation can be considered an aid to the manual reviewers to merge the code with confidence.

## Release

Your product should have short release cycles so that the users get to test the new features without having to wait for long and even contributors feel a sense of satisfaction that their code is deployed to production without having to wait for months.

## Documentation

While we already have a README in place, there should be a link provided to detailed documentation that goes in-depth and explains various modules and code blocks written in the repository. This makes it easier for contributors to understand existing code before adding new code to the system.

This can either be done manually or one can make use of automated document generators like [pdoc](https://pdoc.dev) for python or [compodoc](https://compodoc.app) for Angular.

## Badges

Remember we said at the start that it takes just a minute for someone to decide if your repository is good and worth contributing. Badges help you add that bling to your repository to attract their attention.

You can add badges for anything and everything you wish for, and can explore various badges here: [Shields.io](https://www.shields.io).

Go to this [repository](https://github.com/CSC510-Group-5/URL-Shortner/blob/main/README.md) to see all the badges that can be and have been utilized in the reference repository.

---