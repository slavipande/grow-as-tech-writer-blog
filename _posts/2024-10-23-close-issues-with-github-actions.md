---
layout: post
title:  "How I closed thousands in issues with a GitHub action"
date:   2024-10-23
categories: github
author: Svetoslav Pandeliev
author_linkedin_user: svetoslav-pandeliev
icon: fa-check
hide: true
---

In this blog, I'd like to share how I recently managed to close literally thousands of GitHub issues with a custom GitHub action that I created with the help of AI.

## Intro

Let's start with the issue at hand: I'm administering a couple of GitHub repos that my colleagues are using to write and maintain developer tutorials. Users of these tutorials are also able to open issues in the repos in case they come accross any issues while going through the tutorials. The repos also include some standard GitHub action workflows that check the tutorials when building them after updates and create issues in the repos whenever any problems are identified. At a certain point, a broken tag caused the generation of a large number of issues in each of the repositories. By the time we fix the tag problem, one of the repos had over 5000 issues created and the other one had over 1500 issues created. Such a large number of issues is a problem for every repo because it makes it difficult to detect newly created issues that are actually relevant for the tutorials and need attnetion from the authors. Dealing with all these issues manually was not an options because it meant that I'd have to spent a couple of days doing repetative, dull work by closing the issues in batches of 20 through the GitHub UI. Hence, I decided to look for an alternative solution.

## Research

> Note that this is different than trying to close several issues by merging a PR that's related to them. This is pretty much straightforward and GitHub provides an easy way to mention issues in the PR so they are closed automatically when the PR is merged. See [Linking a pull request to an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) for more details on how to link issues to a PR.

I did a quick internet search and found several different options to solve my problem.

- use GitHub CLI - need to install it, etc
- use a GitHub action - options here were to use the [github stale](https://github.com/actions/stale) action that is available out of the box and also allows for automatically adding a comment to the action before automatically closing it. However I decided to go the other way and directly opened chatGPT (or any company-provided, internal LLM for that matter) and asked if it could help me create a custom github action that will close issues in the repo based on certain criteria. 



## Solution

The process involved a couple of important steps:

1. Constructing a proper prompt

    - Give the AI a role: "Act as an expert devops engineer"
    - Explain what is the task: "I will provide you with the requirements for.... and I'd like you to ..."
    - Mention that I'd like the action to be able to filter issues based on certain criteria - in this case, the criteria was certain combination of words in the title of the issue, mention I'd like to be able to manually run the action instead of it being triggered automatically
    - Ask the AI to include a sample code for the github action, along with comments of what each line does, and with explanation step by step how can I set up and run the action

2. Troubleshooting

    - Continue the conversation with the AI, provide the error message I got along with the script of the action
    - Repeat approach until errors are solved and action works and closes issues
    
3. Improve

    - Ask for ideas to improve the script
    - Add summary and reporting capabilities
    - Add capability to collect logs
    - Repeat troubleshooting approach until it works


## Result

All in all, I spent a day researching, interacting with the AI, testing, and troubleshooting the GitHub action. Then I needed anothe couple of hours to set up and run the action in the different repos where I had a lot of issues to be closed + I had to manually adjust the terms in the search criteria to be able to close issues created by different workflows + I learned something new and further polished my prompting skills.

In comparison, I'd need between two or three days to close all the issues manually and being bored as f.

In addition, now that I have everything set up, I can use the action right away the next time I have to close so many issues which will save me a significant amount of time.



> **Related Info**
>
>   - [Using GitHub Actions for Bulk Resolving](https://timheuer.com/blog/use-github-actions-for-bulk-resolve-issues/)
>   - [How I Bulk Closed 1000+ GitHub Issues with GitHub Actions ](https://dev.to/github/how-i-bulk-closed-1000-github-issues-with-github-actions-d3b)

