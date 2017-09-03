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


### [SimpleHttpClient](https://github.com/Sage-Bionetworks/SimpleHttpClient)
A thin wrapper around Apache's HttpClient to provide a set of simple interfaces to be used for HTTP calls that only transfer json objects.


***


## Other Projects

### [kimyen.github.io](https://github.com/kimyen/kimyen.github.io)
The code base for this site.

## Contact me

[kimyen0816@gmail.com](mailto:kimyen0816@gmail.com)
