---
layout: post
title: "Pre-commit hooks for OPA"
date: 2020-09-01 00:01:00 +0100
categories: tech
tags: pre-commit pre-commit-hooks opa open-policy-agent tooling devops development code-quality
---

One of the things that's _really_ improved my workflow in recent years is using pre-comit hooks for git. Tools that help with code quality and style are everywhere these days and obviously help tremendously in both catching bugs as well as enforcing agreed upon style rules. And while these tools should be included as a natural part of any build pipeline, having to wait for the CI/CD server to build your branch and report back on any code quality issues can be both time consuming and annoying. While it's obvious how to avoid that - by running tests, code quality checks and formatters locally before pushing commits, or at least preparing PR's - I just constantly forget about it. Pre-commit hooks to the rescue!

## The pre-commit framework

<img src="/assets/pre-commit.svg" width="180">

Running hooks in response to events is functionality [built into git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks), but having to manually manage shell scripts for each repository being worked on quickly becomes a real chore, and the idea here is to make us _more_ effective after all. The [pre-commit framework](https://pre-commit.com/) is a "framework for managing and maintaining multi-language pre-commit hooks" and does just that. Though it's called a "framework" it's dead simple to use, simply by following these three steps:

1. Install [pre-commit](https://pre-commit.com/#install).
2. Place a config file (`.pre-commit-config.yaml`) in your project's root directory, pointing out any pre-commit hooks you want to include. There's a [long list](https://pre-commit.com/hooks.html) of ready-made hooks available, so for any language or technology you're working with, chances are good that there's one for your needs.
3. Run `pre-commit install` to install the pre-commit hooks configured in the step above.

That's it! Anytime you run `git commit` from now on, the hooks will be called and any errors reported in hooks like test runners, linters or formatters will now abort the commit, let you fix the issues before re-adding the files to the staging area and reattempt the commit.

## Pre-commit hooks for OPA

Having spent considerable time with [Open Policy Agent](https://www.openpolicyagent.org/) (OPA) in the last year or so, one thing I've really come to miss when authoring and testing policies is pre-commit hooks. OPA comes with a few command line tools to help out during developoment, such as `opa check` to verify syntax, `opa fmt` to format rego policies, and `opa test` to run unit tests. Not having these run by default before commiting has occasionally meant forgetting about it, only to be reminded either by the CI/CD server or a colleague reviewing the policy. We can't have that! So a couple of weeks ago I looked into writing my hooks for this purpose, and it turned out to be dead simple. Adding some fixes based off of real usage in my OPA repos since, and I think they're now in a state where they're good enough for general use. Whether you're new to the pre-commit framework, OPA or both, I hope you'll find the [pre-commit-opa](https://github.com/anderseknert/pre-commit-opa) hooks useful in your OPA projects. 

<img src="/assets/opa-pre-commit.png" width="450">