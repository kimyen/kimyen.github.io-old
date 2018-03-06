---
layout: post
title: kimyen.github.io launched
author: KimYen Ladia
date: 2018-03-05
---

While working on the automated build system for the R client at Sage, I discovered how pass params between Jenkins jobs. In this post, I will talk about why I was interested in this, and what I learned from setting up my builds.

## Why passing params between Jenkins jobs?

The automated build system I worked on is supposed to do the following:
1. One each platform (Linux, Window & Mac):
* Clone and checkout a release candidate branch of a Github repository
* Run `R CMD build` & `R CMD install` to create artifacts
2. Zip the artifacts
3. Generate documentation and update the release candidate branch
4. Push artifacts to our RAN
5. Check that the artifacts can be installed on 3 platforms Linux, Window, and Mac

I have the following Jenkins jobs:

`synapser_staging`
* Runs on 3 slaves (Linux, Window & Mac)
* Executes task #1

`synapser_artifacts`
* Runs on a Mac machine
* Executes task #2 & #3

`synapser_deploy`
* Runs on a slave machine
* Executes #4

`synapser_check`
* Runs on 3 slaves (Linux, Window & Mac)
* Executes #5

`synapser_staging` uses the branch name and the Jenkins job number to determine to version that it's going to build. For example, when the building branch is `v0.1-rc` and the job number is 27, the version that is going to build is `0.1.27` This algorithm allows us to automatically increase the version number without making human mistakes. 

This version number will be used:
* to generate the artifacts (in `synapser_staging`),
* update `Version` in `DESCRIPTION` file, then this change is push back to the building branch (in `synapser_artifacts`),
* and look for which version to check after deployment (in `synapser_check`)

Ideally, I would want to pass the version number from one job to another. 

## How to pass params from one Jenkins job to another?

### Preconditions

To pass params from `synapser_staging` to `synapser_artifacts`, I need the following Jenkins plugins:
* Parameterized Build
* Parameterized Build Trigger 

### Configurations

`synapser_staging` - the giver - is set up with Parameterized Build Trigger in Post Actions section. `synapser_artifacts` - the receiver - is set up with Parameterized Build in the General section. 

### What variables can you pass?

The types of variable that can be passed includes:
* Jenkins environment variables (BUILD_ID, BUILD_NUMBER, ...)
* Params that trigger the giver job (entered from users or passed from another job)
* Github params (BRANCH_NAME)
* Constants (I will talk more about why you need constants).

Constants are useful when you have 2 upstream jobs calling the same downstream job with different variables. For example, my `synapser_check` can be used to check any package version on any RAN. The upstream job would pass it the version number and the RAN URI. In this case, the RAN URI can be a constant defined while configure the giver job with Parameterized Build Trigger.

I hope these information are useful. If you try it, please leave a comment letting me know how it works out for you. 