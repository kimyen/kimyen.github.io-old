---
layout: post
title: synapser Build & Deploy System
author: KimYen Ladia
date: 2018-05-15
---

When I started to work on the `synapser` client, I was given a task to design and implement the client build system. In this post, I will discuss the requirements that was given to me, the practices we established, and how the `synapser` client build system works. 

The slides is available [here](/slides/SynapseRClientBuild&DeploySystem.pdf).

## The Requirements

I received requirements from 3 groups of people:
* The end users;
* The client validators, who are the client users, but are more tech savy and would help us verify that an issue is fixed;
* The developers.

### The End Users' Requirements

1. Sage provides the binaries for each client version. Users should be able to install the client using `install.packages()`, and should not need to install any additional tools (e.g., devtools, C compiler).

### The Validators' Requirements

1. Each version that needs to be validated must have a unique version number. 
2. It should be easy for the validators to install the to-be-validated version and the already-released version, and managing them in their local machine without having one accidentally overwriting another.
3. The Github repository that hosts the client source code must follow standard R packages and easy to navigate between different versions. 

### The Developers' Requirements

1. The client version should be automatically increased to eliminate mistakes made by the developers.
2. The build & deployment system must be easy to use and maintenance. 
3. The documentation must be updated automatically to prevent content out of date.
4. The deployment process must check that the artifacts are available after the deployment, and can be installed on Mac, Linux, and Windows.

I took the requirements above and played with many different plugin and settings in Jenkins. There were so many different ways to setup the Github repository and Jenkins jobs to achieve them. To narrow down the implementation, we establish our practice.

## Our Practices

### R Packages Practices

#### Version

Our package version has 3 parts: `<major>.<minor>.<dev>`
A product manager will determine the `<major>.<minor>` part. The build system will automatically increase the `<dev>` number.

#### RAN and Documentation

We use Github Pages to host our R packages, and documentation.
Our RAN is setup in an CRAN-like repository, enabling users to install R packages by executing `install.packages()`.
We setup 2 types of RAN:

* ran: hosting released packages
* staging-ran: hosting to-be-validated packages

### Release Process

1. Identify the release candidate
2. Developerment work
3. Build and deploy artifacts to staging-ran
4. Validation
5. Deploy tested artifacts to ran

### Github Practices

#### Github Branches

We have 3 types of Github branches:

1. `master` branch: keeping track of the latest released version.
2. `develop` branch: keeping track of the latest development work.
3. release-candidate branches: keeping track of each to-be-validated version.

#### Github Tags

We created a tag for each version that is ever built.

### Development Practices

* Each developer folk the central repository and add new feature to their folk.
* Each developer is responsible to make sure that their contribution does not include broken code by running their own private builds before making pull request against the central repository's `develop` branch.
* Each pull request that is merged to the `develop` branch will trigger a develop build that attempts to build the artifacts and run all tests on 3 platforms: Mac, Linux, and Windows.

### Deployment Practices

Each deployment ensures that the binaries are available and installable for Mac and Windows. The source code is available and installable for Linux.

## The Build & Deploy System

Now that we setup all the practices above, it's very straight forward what we need to make everything works with a few clicks. I setup 3 types of builds:

* The dev builds,
* The staging builds, and
* The prod builds

### The dev builds

The dev builds are used to ensure that artifacts can be built on 3 platforms: Mac, Linux, and Windows; and all tests are passed.

The dev build is used by each developer for their private builds, and for the central repository's `develop` branch upon pull request merge events.

### The staging builds

The staging build is triggered when we are ready to enter validation phase. It checks out code from the central repository's release candidate branch, and performs the following tasks:

* Build the artifacts on 3 platforms: Mac, Linux, and Windows
* Update version and documentation on the release candidate branch
* Deploy the artifacts to staging-ran
* Ensure that the artifacts are installable by 3 platforms: Mac, Linux, and Windows from `staging-ran`

### The prod builds

The prod build is triggered when we are ready to release a version to `ran`. It performs the following tasks:

* Deploy the built artifacts to `ran`
* Ensure that the artifacts are installable by 3 platforms: Mac, Linux, and Windows from `ran`

## Notes & Documentation

while working on this task, I wrote multiple documentation and putting build script in a Github repository:

* [The design](hips://sagebionetworks.jira.com/wiki/spaces/SYNR/ pages/151420929/ synapser+dev+staging+validation+release)
* [The builds](hips://sagebionetworks.jira.com/wiki/spaces/SYNR/ pages/154861569/Jenkins+Builds+- +Info+and+Maintenance)
* [The scripts](hips://github.com/Sage-Bionetworks/CI-Build-Tools)
