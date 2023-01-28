---
title: "What actually is Database Sharding?"
categories: [sql, database, sharding, benefits-of-sharding, sidsblog]
tags: [sql, database, sharding, advantages, disadvantages, sidsblog]
date: 2021-10-14T17:26:04+05:30
description: "This tutorial will clear all your doubts regarding the Database Sharding and do you actually need it"
author: Siddhant Mulajkar
draft: false
---

##### How often do you shard your database?

##### Do you prematurely shard?

##### Do you actually need that for your database?🤔

--

***Your application is growing. It has more active users, more features, and generates more data every day.***

***Your database is now becoming a bottleneck for the rest of your application. Database sharding could be the solution to your problems.***

### But Wait...


![Database Sharding](/images/databasesharding/dbshardingintro.jpg)

---

![Database Sharding1](/images/databasesharding/dbshard.png)

---



### Q) What is Database Sharding?

Sharding is a method for distributing a single dataset across multiple databases, which can then be stored on multiple machines. 

This allows for larger datasets to be split in smaller chunks and stored in multiple data nodes, increasing the capacity.

Sharding is a form of scaling known as horizontal scaling or scale-out, as additional nodes are brought on to share the load. 

Horizontal scaling allows for near-limitless scalability to handle big data and intense workloads.

![Horizontal Sharding](/images/databasesharding/horizontalscale.jpeg)

---

It can be helpful to think of horizontal partitioning in terms of how it relates to vertical partitioning.

![Types of Partition for Sharding](/images/databasesharding/partitioneg.png)

---

***Database shards exemplify a shared-nothing architecture.😦***

***This means that the shards are autonomous, they don’t share any of the same data or computing resources.***

--

### Q) How Does Sharding Work?

To shard a database, we must answer several fundamental questions.

- First, how will the data be distributed across shards?

- Second, what types of queries will be routed across shards?

- Finally, how will these shards be maintained?


First, how will the data be distributed across shards? This is the fundamental question behind any sharded database. The answer to this question will have effects on both performance and maintenance. More detail on this can be found in the “Sharding Architectures and Types” section.

Second, what types of queries will be routed across shards? If the workload is primarily read operations, replicating data will be highly effective at increasing performance, and you may not need sharding at all. In contrast, a mixed read-write workload or even a primarily write-based workload will require a different architecture.

Finally, how will these shards be maintained? Once you have sharded a database, over time, data will need to be redistributed among the various shards, and new shards may need to be created. Depending on the distribution of data, this can be an expensive process and should be considered ahead of time.

-------------------------------------------------------------------------------

### Q) Do You Need Database Sharding?

Whether or not we should implement a sharded database architecture has always been a matter of debate.

Some see sharding as an inevitable outcome for databases that reach a certain size, while others see it as a headache that should be avoided unless it’s absolutely necessary, due to the operational complexity that sharding adds.

--

**Because of this added complexity, sharding is usually only performed when dealing with very large amounts of data. Here are some common scenarios where it may be beneficial to shard a database:**

- The amount of application data grows to exceed the storage capacity of a single database node.
- The volume of writes or reads to the database surpasses what a single node or its read replicas can handle, resulting in slowed response times or timeouts.
- The network bandwidth required by the application outpaces the bandwidth available to a single database node and any read replicas, resulting in slowed response times or timeouts.

--


***Before sharding, you should exhaust all other options for optimizing your database. Some optimizations you might want to consider include:***

 - **Setting up a remote database** If you’re working with a monolithic application in which all of its components reside on the same server, you can improve your database’s performance by moving it over to its own machine. This doesn’t add as much complexity as sharding since the database’s tables remain intact. However, it still allows you to vertically scale your database apart from the rest of your infrastructure.

- **Implementing caching** If your application’s read performance is what’s causing you trouble, caching is one strategy that can help to improve it. Caching involves temporarily storing data that has already been requested in memory, allowing you to access it much more quickly later on.

- **Creating one or more read replicas** Another strategy that can help to improve read performance, this involves copying the data from one database server (the primary server) over to one or more secondary servers. Following this, every new write goes to the primary before being copied over to the secondaries, while reads are made exclusively to the secondary servers. Distributing reads and writes like this keeps any one machine from taking on too much of the load, helping to prevent slowdowns and crashes. **Note that creating read replicas involves more computing resources and thus costs more money, which could be a significant constraint for some.**

- **Upgrading to a larger server** In most cases, scaling up one’s database server to a machine with more resources requires less effort than sharding. As with creating read replicas, an upgraded server with more resources will likely cost more money. Accordingly, you should only go through with resizing if it truly ends up being your best option.

--

**Bear in mind that if your application or website grows past a certain point, none of these strategies will be enough to improve performance on their own. In such cases, sharding may indeed be the best option for you.**

---

### Advantages of Database Sharding:

Sharding allows you to scale your database to handle the increased load to a nearly unlimited degree by providing increased read/write throughput, storage capacity, and high availability. 

Let’s look at each of those in a little more detail.


- Increased Read/Write Throughput — 

By distributing the dataset across multiple shards, both read and write operation capacity is increased as long as read and write operations are confined to a single shard.


- Increased Storage Capacity — 

Similarly, by increasing the number of shards, you can also increase overall total storage capacity, allowing near-infinite scalability.


- High Availability — 

Shards provide high availability in two ways. 
1) Since each shard is a replica set, every piece of data is replicated.
2) Even if an entire shard becomes unavailable since the data is distributed, the database as a whole still remains partially functional.

---

### Disadvantages of Sharding:

Sharding does come with several drawbacks, namely overhead in query result compilation, the complexity of administration, and increased infrastructure costs.


- Query Overhead — 

Each sharded database must have a separate machine or service which understands how to route a querying operation to the appropriate shard. 

This introduces additional latency on every operation. 


Furthermore, if the data required for the query is horizontally partitioned across multiple shards, the router must then query each shard and merge the result together. 

This can make an otherwise simple operation quite expensive and slow down response times.


- Complexity of Administration — 

With a single unsharded database, only the database server itself requires upkeep and maintenance. 

With every sharded database, on top of managing the shards themselves, there are additional service nodes to maintain. 


Plus, in cases where replication is being used, any data updates must be mirrored across each replicated node.

Overall, a sharded database is a more complex system that requires more administration.


- Increased Infrastructure Costs — 

Sharding by its nature requires additional machines and compute power over a single database server. 

While this allows your database to grow beyond the limits of a single machine, each additional shard comes with higher costs.


- Another major drawback is that once a database has been sharded, it can be very difficult to return it to its unsharded architecture.

- A final disadvantage to consider is that sharding isn’t natively supported by every database engine.


---

***Having considered the pros and cons, let’s move forward and discuss the  implementation of few different architectures for sharded databases,***

in a new post...[database sharding architecture]({{< relref "posts/database-sharding-architectures.md">}})

