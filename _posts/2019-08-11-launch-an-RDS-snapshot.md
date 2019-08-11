---
layout: post
title: Launch an RDS Snapshot
author: KimYen Ladia
date: 2019-08-11
---

Working in a small team means that most of the time, we don't have resources to solve all of the use cases. One of the skills that I learned working at Sage is to figure out the least amount of work I can do to unblock most people.

# Background & Use Cases

The Synapse Data Warehouse is hosted on an AWS RDS. We have a fleet of workers that imports data to the Data Warehouse continuously. We also have number of clients connections to the RDS, and execute query continuously.

Once in a while, some data engineers need to run a few custom queries against the Data Warehouse. Why? They are getting usage stats that Synapse has not yet provided. The real solution would be to add a new feature to Synapse that reports the usage stats. 

To add a new feature to Synapse, it requires a little bit of design, architecting the backend services, adding new schema in Synapse, and possibly refactor some backend code. After testing the services, the clients need to expose the new services, and possibly go through a few iterations until the users like how it looks.

How long does the whole process takes? A couple months, probably.

At the mean time, the data engineers are frustrated with their queries running very slowly. Why is it slow? The data warehouse was built with all of the data for all of the projects. It solved true Synapse Admin use cases. A data engineers only query for a single project. In their query, they want to look at only data for a single project, join with data on a single project. But a data engineer does not have and should not have write access/ create table in the Data Warehouse RDS. They can simply READ. So their queries are insufficient against the given schema.

Only if the data engineers can have their own copies of the Data Warehouse, where they can create tables that only contains data for a single project, add indexes on columns that they need to filter, and do not add workload to the original/ main data warehouse or modifying it in anyway, then we can solve this problem temporaly before we have a new shiny feature in Synapse that reports stats.

# The Builds

What is the Data Warehouse copies idea? and how does it work?

We would need a system that the data engineers can login securely, click a button to get their copy of the latest version of the data warehouse. Then after they finish their report, click another button to clean up the copy.

We use a dedicated Jenkins server to implement this. Only admin can configure jobs. Data engineers each has their own account. They can only login if they are under our private network. And the only permission a data engineer has is to start a job.

See instruction here: https://sagebionetworks.jira.com/wiki/spaces/DW/pages/796819457/Warehouse+Snapshot

# The Implementation

But what happens when a data engineer starts a Jenkins job to launch a snapshot?

We turned on automatic snapshot for the Data Warehouse. Every day, a new snapshot is captured. When launching a snapshot, the Jenkins job literraly chooses the latest snapshot to launch as a new RDS. It also grant access to a new MySQL user with credentials taken from data engineer prior to launch time.

This way, each snapshot that is launched is only available for a single data engineer. When he/she connects to the copied RDS, he/she would have all the access required to create new tables and add indexes. 

The code: https://github.com/Sage-Bionetworks/CI-Build-Tools/blob/master/warehouse/dw_snapshot.py
