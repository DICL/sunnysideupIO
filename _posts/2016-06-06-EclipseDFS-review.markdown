---
layout: post
title:  "How would you efficiently store a file of 100 TeraBytes in your cluster?"
date:   2016-06-06 17:07:08 +0900
categories: jekyll update
---

As a Big Data entreprise, since the development of our MapReduce Engine, we faced the problem of
managing very large files. Today's distributed file systems (DFS) brings us infity options and features to 
face this problem. Unfortunatelly, none of those DFS did satisfy our demanding needs.

Then, Once again in the software industry, we decided to reinvent the wheel and we implemented our custom DFS.

# What is EclipseDFS?
EclipseDFS is a lightweight ad-hoc distributed file system (DFS). But why? we believed that current DFS solutions does not scale
well nor use efficiently cache and other performance tools.

# Why would your organization use EclipseDFS?
If your organization needs to store large amounts of data, using a DFS for storing the data might be the right thing to do, 
any DFS would satisfy most the industries needs. Differences are upon scalability, performance, and safety. Here are
EclipseDFS's four main advantages:

- It's decentralized, there is no overhead upon scaling.
- It's an user-space application, there is no need to load a driver in order to use it.
- It's fast, actually very fast, thanks to its distributed cache and asynchronous architecture.
- It's open source! you are free to modify it and adapted to your business.

For those who are not familiar with DFS, here is brief explanation of how DFS works: A DFS divides the files into blocks 
which are distributed (evenly) among the different servers.

# Usage

EclipseDFS supports the basic operations that you might expect in a file system. Here is all the possible client invocation.

{% highlight sh%}
$ dfs put|get|rm|list|cat|info|format|pget|update|append
{% endhighlight %}
