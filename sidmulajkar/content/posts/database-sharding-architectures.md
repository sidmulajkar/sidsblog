---
title: "Boosting Performance through Effective Database Sharding Architectures for Optimal Optimization"
categories: [sql, database, sharding, benefits-of-sharding, architecures, sidsblog]
tags: [sql, database, sharding, advantages, disadvantages, sharding-architectures, sidsblog]
date: 2021-10-17T17:26:04+05:30
description: "This tutorial will clear all your doubts regarding the Database Sharding Architectures and how to implement them."
author: Siddhant Mulajkar
draft: false
---

### Once you’ve decided to shard your database, the next thing you need to figure out is how you’ll go about doing so.

Your application suddenly becomes popular. Traffic and data are starting to grow, and your database gets more overloaded every day. 

People on the internet tell you to scale your database by sharding, but you don’t know what it means.

![Database Sharding1](/images/shardingarch/shard1.png)

---

If you haven't read the last blog post and want to know more about Database Sharding check the previous blog > [What is Database Sharding]({{< relref "posts/what-is-database-sharding.md" >}})

### Driving Principles:

To compare the pros and cons of each sharding strategy, We will use the following principles.

- How the data is read

- How the data is distributed

- Re-distributing data

1. **How the data is read** — Databases are used to store and retrieve data. If we don’t need to read data at all, we can simply write it to /dev/null. If we only need to batch process the data once in a while, we can append to a single file and periodically scan through them. Data retrieval requirements (or lack thereof) heavily influence the sharding strategy.

2. **How the data is distributed** — Once you have a cluster of machines acting together, it is important to ensure that data and work is evenly distributed. Uneven load causes storage and performance hotspots. Some databases redistribute data dynamically, while others expect clients to evenly distribute and access data.

3. Once sharding is employed, **redistributing data** is an important problem. Once your database is sharded, it is likely that the data is growing rapidly. Adding an additional node becomes a regular routine. It may require changes in configuration and moving large amounts of data between nodes. It adds both performance and operational burden.

--

### Common Definitions:

Many databases have their terminologies.

Shard or Partition Key is a portion of the primary key that determines how data should be distributed. A partition key allows you to retrieve and modify data efficiently by routing operations to the correct database.


Shard or Partition Key is a portion of the primary key that determines how data should be distributed. 

A partition key allows you to retrieve and modify data efficiently by routing operations to the correct database.

---

***Once you’ve decided to shard your database, the next thing you need to figure out is how you’ll go about doing so.***

When running queries or distributing incoming data to sharded tables or databases, it must go to the correct shard.

--

### 1. Key Based Sharding: 

It is also known as hash-based sharding, involves using a value taken from newly written data — such as a customer’s ID number, a client appl’s IP address, a ZIP code, etc. — and plugging it into a hash function to determine which shard the data should go to.

![Key Based Sharding](/images/shardingarch/shardkey.png)


While key-based sharding is a fairly common sharding architecture, it can make things tricky when trying to dynamically add or remove additional servers to a database.


As you add servers, each one will need a corresponding hash value, and many of your existing entries, if not all of them, will need to be remapped to their new, correct hash value and then migrated to the appropriate server.


As you begin rebalancing the data, neither the new nor the old hashing functions will be valid. 

Consequently, your server won’t be able to write any new data during the migration and your application could be subject to downtime.


The main appeal of this strategy is that it can be used to evenly distribute data to prevent hotspots. Also, because it distributes data algorithmically, there’s no need to maintain a map of where all the data is located.

---

### 2. Range/Dynamic Based Sharding:

This sharding involves sharding data based on the ranges of a given value. To illustrate, let’s say you have a database that stores information about all the products within a retailer’s catalog. You could create a few different shards.

![Range Based Sharding](/images/shardingarch/rangebased.png)

The main benefit of range-based sharding is that it’s relatively simple to implement. 

Every shard holds a different set of data but they all have an identical schema as one another, as well as the original database. 

The application code just reads which range the data falls into and writes it to the corresponding shard.

On the other hand, range-based sharding doesn’t protect data from being unevenly distributed, leading to the aforementioned database hotspots.

---

### 3. Directory-Based Sharding:

To implement this sharding, one must create and maintain a lookup table that uses a shard key to keep track of which shard holds which data. In a jiffy, a lookup table is a table that holds a static set of information about where specific data is found.

![Directory Based Sharding](/images/shardingarch/dirbased.png)


The main appeal of directory-based sharding is its flexibility.
Range-based sharding architectures limit you to specifying ranges of values, while key-based ones limit you to using a fixed hash function which, as mentioned previously, can be exceedingly difficult to change later.


Directory-based sharding, on the other hand, allows you to use whatever system or algorithm you want to assign data entries to shards, and it’s relatively easy to dynamically add shards using this approach.

---

#### Other Sharding Architecture's

### Entity-/Relationship-Based Sharding

Entity-based sharding keeps related data together on a single physical shard. In a relational database (such as PostgreSQL, MySQL, or SQL Server), related data is often spread across several different tables.

For instance, consider the case of a shopping database with Users and Payment Methods. Each user has a set of payment methods that is tied tightly with that user. As such, keeping related data together on the same shard can reduce the need for broadcast operations, increasing performance.


### Geography-Based Sharding

Geography-based sharding, or geosharding, also keeps related data together on a single shard, but in this case, the data is related by geography. This is essentially ranged sharding where the shard key contains geographic information and the shards themselves are geo-located.

For example, consider a dataset where each record contains a “country” field. In this case, we can both increase overall performance and decrease system latency by creating a shard for each country or region, and storing the appropriate data on that shard. This is a simple example, and there are many other ways to allocate your geoshards which are beyond the scope of this article.

---

### Conclusion:

***Sharding is a great solution for applications with large data requirements and high-volume read/writes workloads, but it does come with additional complexity.*** 

***Consider whether the benefits outweigh the costs or there is a simpler solution even before you begin implementing.***

--

If you haven't read the last blog post and want to know more about Database Sharding check the previous blog > [What is Database Sharding]({{< relref "posts/what-is-database-sharding.md" >}})


---

### Read More Blogs related to:

***[database]({{< relref "/tags/database/">}}) / [linuxsubsystem(wsl)]({{< relref "/tags/linuxsubsystem/">}}) / [flutter installation]({{< relref "/tags/flutter-installation">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberrypi">}})*** 

--