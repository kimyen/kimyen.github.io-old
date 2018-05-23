---
layout: post
title: Convert data between R and Python
author: KimYen Ladia
date: 2018-05-22
---

One of the technology platforms that we develop at Sage Bionetworks is Synapse. Besides the Web client, Synapse also supports R and Python clients. These programatic clients were developed independent of each others and eventually diversed.

To eliminate the engineering efforts to maintain both clients, we decided to add new features to one client, and "auto-generate" the other client.

My collegue figured out that it would be easier to wrap Python in R than to do it the other way around. 

The idea is that our R users would write code in R. It will then turn around and call an existing Python function. The Python function is executed in a Python session. When the Python function returns, we would convert the returned value into an R value.

At the time we were trying to solve this problem [`reticulate`](https://github.com/rstudio/reticulate) hasn't exist yet. So we found and use [`pythonInR`](https://bitbucket.org/Floooo/pythoninr/) package.

This post is to capture my notes on converting data between R and Python. It's not a complete solution yet.

# R Data Types

There are so many different sites offer tutorials on R Data Types. In this section, I only talks about the most basic of all:

* Vectors
* Lists
* Objects

And the following atomic vector types:

* `NULL`
* `logical`
* `integer`
* `real`
* `complex`
* `string`

Notes that I intentionally left out `raw` atomic type, because none of our use cases require us to handle `raw` type (yet).

Interesting notes about R Data Types:

* A `list` is a `vector`, but a `vector` is not a `list`.
* A single value is a `vector` of length 1.
* Beside `True` and `False`, `NA` is also a `logical`.
* A `vector` has no `NULL`.
* Both `vector` and `list` may have names. However, the names do not have to be unique.

< to be continued >

