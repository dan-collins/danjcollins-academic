---
title: Leveraging Concurrency, Channels, and Error Groups in Go to Handle
  Queries on Multiple Databases
subtitle: Go can help you get information from multiple sources...quickly!
date: 2020-10-28T14:24:28.689Z
draft: true
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

#### Concepts

I rely on 3 main concepts for this implementation (you can probably guess them from the title):

1. **Concurrency**

   One of the most important things was that this had to be fast. I didn't want the data merge that I was doing to take 20 minutes to run. In order to get that much data quickly, I relied on Go's great concurrency goroutine functionality. 
2. **Channels**

   When you use concurrency in Go, you have to be careful to use the right data structures. Channels are great ways to safely persist data among all the concurrent goroutines that are running. Buffered channels also help to be used like a semaphore concept to limit the total number of concurrent goroutines that can run at a time.
3. **Error Groups**

   When you work concurrently, errors can be hard to manage because there are many isolated tasks being completed that are not necessarily related. Go luckily has a nice Error Group (<https://pkg.go.dev/golang.org/x/sync/errgroup>) library for managing errors that occur in these concurrent processes.