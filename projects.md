---
layout: page
title: Projects
permalink: /projects/
---

### [Synapse-Repository-Services](https://github.com/Sage-Bionetworks/Synapse-Repository-Services) 
The code base for [Synapse.org](https://www.synapse.org/) server and its Java client.

#### Discussion Feature
* Enabled discussion between Synapse users and Synapse Support Team ([Synapse Help Forum](https://www.synapse.org/#!SynapseForum:default)), between
Dream Challenge participants and organizers including [The Digital Mammography Dream Challenge](https://www.synapse.org/#!Synapse:syn4224222/discussion/default) , between Sage and data contributors including  [the Bridge - Lily project](https://www.synapse.org/#!Synapse:syn6101466/discussion/default) , and endless possibilities in every single projects created and shared by users.
* [Learn more](http://hud.rel.rest.doc.sagebase.org.s3-website-us-east-1.amazonaws.com/#org.sagebionetworks.repo.web.controller.DiscussionController)

#### Access Control Tool
* Enabled the Access and Compliance Team to manage the terms and requirements, to track, review, reject,
and grant access to a group of users within Synapse.
* Streamlined the process to participate in Dream Challenges including the [Parkinsons Disease Digital
Biomarker DREAM Challenge](https://www.synapse.org/#!Synapse:syn8717496/wiki/422884) , and [the NIH Data Commons](https://www.youtube.com/watch?v=P0bYDI2QHZM&t=24s).
* [Learn more](http://hud.rel.rest.doc.sagebase.org.s3-website-us-east-1.amazonaws.com/#org.sagebionetworks.repo.web.controller.DataAccessController)

#### Refactor Java Client
* Rewrote the Synapse Java Client implementation to use [SimpleHttpClient](https://github.com/Sage-Bionetworks/SimpleHttpClient).
* Enabled other applications including the [Bridge Exporter](https://github.com/Sage-Bionetworks/Bridge-Exporter) that is using the Synapse Java Client to programmatically restart its connection pool when an existing connection pool is saturated because of a connection leak or other reasons.


### [Synapse-Warehouse-Workers](https://github.com/Sage-Bionetworks/Synapse-Warehouse-Workers)
Data collected from [Synapse.org](https://www.synapse.org/) server are stored in S3. [Synapse-Warehouse-Workers](https://github.com/Sage-Bionetworks/Synapse-Warehouse-Workers) imports the captured snapshots into its partitioned MySQL database and pre-processes them, allowing its client to query against these data for reports.

[Learn more](https://sagebionetworks.jira.com/wiki/spaces/DW/pages/82116618/MySQL+Data+Warehouse)


### [SynapseWebClient](https://github.com/Sage-Bionetworks/SynapseWebClient)
The web client of [Synapse.org](https://www.synapse.org/).

* UI for Discussion feature
* UI for Docker feature


### [SimpleHttpClient](https://github.com/Sage-Bionetworks/SimpleHttpClient)
A thin wrapper around Apache's HttpClient to provide a set of simple interfaces to be used for HTTP calls that only transfer json objects.


### [synapser](https://github.com/Sage-Bionetworks/synapser)
The R client of [Synapse.org](https://www.synapse.org/).

#### The Build System
* Proposed [the plan](https://sagebionetworks.jira.com/wiki/spaces/SYNR/pages/151420929/synapser+dev+staging+validation+release) for how to develop, build, and release [synapser](https://github.com/Sage-Bionetworks/synapser). 
* Organized the builds on Jenkins and wrote [documentation for maintenance](https://sagebionetworks.jira.com/wiki/spaces/SYNR/pages/154861569/Jenkins+Builds+-+Info+and+Maintenance).
* Organized the Gists used in the build system into a Github repository called [CI-Build-Tools](https://github.com/Sage-Bionetworks/CI-Build-Tools).
* [Slides](/slides/SynapseRClientBuild&DeploySystem.pdf)

### [PythonEmbedInR](https://github.com/Sage-Bionetworks/PythonEmbedInR)
Folked from PythonInR repository. 

#### Data Conversion
* Added `testthat` and a set of test cases to ensure the conversion behaviors.
* Fixed bugs related to converting data from Python 3 to R.
* Ensured private methods in Python object are not exposed in R.

#### Python Package Wrapper Utilities
* Extended PythonEmbedInR package to include utilities functions that generate R wrappers, and documentations for Python packages.
* Allowed R users to select functions, classes, Enums, and module to expose in R.
* Enabled R users to intercept and alter the returned object in R.
* Provided instructions and examples on how to create an R package by wrapping a Python package.


### [synapsePythonClient](https://github.com/Sage-Bionetworks/synapsePythonClient)
The Python client of [Synapse.org](https://www.synapse.org/).

#### Enable Single Thread
* Added the ability to use the Synapse Python client in a single threaded environment (in synapser).

#### House Keeping
* Stablized the integration tests.
* Improve development builds from taking several days to taking ~20 minutes.
* Simplified integration tests for using only one test user, only exercising the http call, not the server's logic. 
* Directed the integration tests to build against a development stack.

#### Communication Channels
* Exposed released notes on the Synapse Python client docs.
* Highlighted deprecated methods in the Synapse Python client docs.


### IT
Collections of IT tasks.

#### Test User for Development Stack
* Added a build to create a test user for a development stack. 
* Allowed client builds to run integration tests against the development stack.

***


## Other Projects

### [kimyen.github.io](https://github.com/kimyen/kimyen.github.io)
The code base for this site.

## Contact me

[kimyen0816@gmail.com](mailto:kimyen0816@gmail.com)
