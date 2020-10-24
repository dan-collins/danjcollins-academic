---
title: Leveraging Concurrency, Channels, and Wait Groups in Go to Handle Queries
  on Multiple Databases
subtitle: Go can help you get information from multiple sources...quickly!
date: 2020-10-30T17:13:11.227Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
#### Overview

Have you ever needed to get the same structure of data from many separate sources? For instance, what if you needed to get item information from many instances of the same E-Commerce platform. That actually turned out to be what I needed and sparked this post. I hope that this paradigm I am about to describe can help someone who is looking for a way to quickly and efficiently query data from multiple database servers with Go. This article will not go into setting up Go but if this is your first time seeing it, I highly recommend checking out the [Tour of Go](https://tour.golang.org) to get started. To get the most out of this article, it is good to have an understanding of Go syntax, goroutines, and channels.

#### Assumptions

There are a few certain things that this specific implementation relies on. With some tweaking I believe that many of the concepts could be leveraged outside of this use case but nevertheless, assume the following:

1. The data across the various databases existed in the same structure/tables per instance.
2. All of the database instances can be reached via TCP on a specific port using a username and password for authentication.