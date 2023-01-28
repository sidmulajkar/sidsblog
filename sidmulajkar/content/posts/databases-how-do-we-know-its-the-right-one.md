---
title: "Databases! How do we know it's the right one? "
categories: [factors, vertical scaling, horizontal scaling, data-structure, database, sidsblog]
tags: [factors, vertical scaling, horizontal scaling, data-structure, database, sidsblog]
date: 2021-12-23T17:26:04+05:30
description: "This tutorial will help you understand what factors to consider before the selecting the database."
author: Siddhant Mulajkar
draft: false
---


### Choosing the Best Database?

![What to Select](/images/factorsofdatabase/sqlvsnosql.png)

---


**Whether you are an experienced software engineer or a student doing a university project, at some point we will need to choose a DB for our project.**

***Choosing the right kind of database always requires some consideration.***

--

##### First of all, databases will not impact our functional requirements.
##### Whichever database we use can still achieve our functional requirements somehow, but at the cost of huge performance degradation.

So when we say requirement, we usually mean ***non-functional*** requirements

---

### Factors:

```
- Structure of the data
- Query pattern
- Amount or scale that we need to handle
```
--

- How much data do we expect to store when the application is mature?

- How many users do we expect to handle simultaneously at peak load?

- What availability, scalability, latency, throughput, and data consistency does our application need?

- How often will our database schemas change?

- What is the geographic distribution of our user population?

- What is the natural “shape” of our data?

- Does our application need online transaction processing (OLTP), analytic queries (OLAP), or both?

- What ratio of reads to writes do we expect in production?

- What are our preferred programming languages?

- How strict are we with invalid data being sent to our database? (Ideally, we are very strict and do server-side data validation before persisting it to our database)

--

*These are some of the factors we need to consider when selecting which database to use.*


A bonus reason for understanding the different DBs and their properties is that it’s quite a common question in job interviews!

--------------------------------------------------------------------------


#### How to Choose the Right Type of Database?

*Given that there are so many different types of databases, choosing one can be confusing.*

Consider these factors that we should keep in mind when selecting a database management system:


1. **Atomicity**

    If atomicity is a top priority for us, then we need to stick to a relational database. 

    Atomicity in database management promotes consistency in a database. It rests on the principle of atomic transactions.


2. **Vertical or horizontal scaling**

    If the data strategy rests on vertical scaling, then a relational database is fine.

    Vertical scaling adds more computing power to a server instead of adding more servers to the system.


    It is preferred when there are a limited number of users and not a lot of querying involved. In that sense, vertical scaling might be suitable for business-facing startups.

    The basic advantages of vertical scaling are speed and simplicity.

--

**Horizontal scaling:**

If we expect higher loads in the scale of users or querying, horizontal scaling is a much cheaper solution. 

NoSQL databases employ horizontal scaling. Instead of adding more compute power to a server, they distribute the load across servers.

--

3. **Speed**

    If speed is more important than ACID compliance, a non-relational database, such as a document database, is a better bet.

    For instance, in the case of real-time data, such as sensor data, some compromise in data integrity can be tolerated in favor of speed.


    In a non-relational database, each record is an independent entity. Thus, it is possible to run multiple queries simultaneously irrespective of the size of the database.

---

### SQL-based vs NoSQL-based

Before diving into the most popular modern database options in the next post, it's important to understand the difference.

We will see SQL vs NoSQL specific databases in upcoming posts.

*https://www.integrate.io/blog/which-database/*


***When choosing a modern database, one of the biggest decisions is picking a relational (SQL) or non-relational (NoSQL) data structure. While both are viable options, there are key differences between the two that users must keep in mind when making a decision.***

Still, each year, NoSQL-based non-relational database management systems are becoming more popular—particularly because data scientists want to expose their machine learning business analytics tools to more unstructured data. Let's look at how these database styles differ.

---

### Relational Database Management Systems (SQL-Based)

Relational database management systems (RDBMSs) use SQL, a database management language that offers a highly organized and structured approach to information management.

Similar to the way a phone book has different categories of information (name, number, address, etc.) for each line of data, relational databases apply strict, categorical parameters that allow database users to easily organize, access, and maintain information within those parameters.

***The primary reasons why SQL-based RDBMSs continue to dominate are:***


(1) they are highly stable and reliable.

(2) they adhere to a standard that integrates seamlessly with popular software stacks like LAMP.

--------------------------------------------------------------------------

***RDBMS advantages:***

- ACID compliance: If a database system is "ACID compliant," it satisfies a set of priorities that measure the atomicity, consistency, isolation, and durability of database systems. The more ACID-compliant a database is, the more it serves to guarantee the validity of database transactions, reduce anomalies, safeguard data integrity, and create stable database systems. Generally, SQL-based RDBMSs achieve a high level of ACID compliance, but NoSQL databases give up this distinction to gain speed and flexibility when dealing with unstructured data.
    
- Ideal for consistent data systems: With a SQL-based RDBMS, our information will remain in the structure you originally create. If we don't need a dynamic information system for massive amounts of data—and we're not dealing with numerous data types — an RDBMS offers great speed and stability.
    
- Better support options: Because RDBMS databases have been around for over 40 years, it's easier to get support, add-on products, and integrate data from other systems.

--


***RDBMS disadvantages:***

- Scalability challenges and difficulties with sharding: RDBMSs have a more difficult time scaling up in response to massive growth compared to NoSQL databases. These databases also present challenges when it comes to sharding. Sharding is the process of dividing a large database into smaller parts for easier management. If we're dealing with a conservative database that we don't expect to change a lot in the years ahead, the sharding and scaling challenges related to RDBMS solutions may never apply to us. On the other hand, if we plan to scale up and grow in the years ahead, a non-relational database system (NoSQL-based) could be a better match for our needs.
    
- Less efficient with NoSQL formats: Most RDBMSs are now compatible with NoSQL data formats, but they don't work with them as efficiently as non-relational databases.

---


**Non-Relational Database Systems (NoSQL-based)**

***Imagine a task of managing large amounts of unstructured data, such as text from emails and customer surveys, data collected by a network of mobile apps, or random social media information. The information is unorganized.***

***There isn't a clearly-defined schema like you would find in an RDBMS. We can't store such information in an RDBMS. But we can store it with a non-relational (or NoSQL) database system.***

--

**Non-relational databases** let us organize information in a looser fashion—kind of like dropping the information in different file folders. This is important for two reasons: 

(1) we can store unstructured information and expose it to powerful business intelligence systems that will analyze it with AI algorithms.

(2) we can store unstructured data that you plan to structure later.

Non-relational databases also work with NoSQL formats like JSON, which has become essential for web-based applications that let websites update "live" without needing to refresh the page.

---

***Non-relational DBMS advantages:***

- Excellent for handling "big data" analytics: The main reason why NoSQL databases are becoming more popular is that they remove the bottleneck of needing to categorize and apply strict structures to massive amounts of information. NoSQL databases like HBase, Cassandra, and CouchDB support the speed and efficiency of server operations while offering the capacity to work with large amounts of data.

- No limits on types of data you can store: NoSQL databases give you unlimited freedom to store diverse types of data in the same place. This offers the flexibility to add new and different types of data to your database at any time.

- Easier to scale: NoSQL databases are easier to scale. They're designed to be fragmented across multiple data centers without much difficulty.

- No data preparation required: When there isn't time to design a complex model, and you need to get a database running fast, non-relational databases save a lot of time.

--

***Non-relational DBMS disadvantages:***

- More difficult to find support: Because the NoSQL community doesn't have years of history and development behind it, it could be more difficult to find experienced users when you need to troubleshoot.

- Lack of tools: Since the system is relatively new compared to SQL-based RDBMS solutions, there aren't as many tools to assist with performance testing and analysis.

- Compatibility and standardization challenges: Newer NoSQL database systems also lack the high degree of compatibility and standardization offered by SQL-based alternatives. We may find that the data in our non-relational database management system doesn't readily integrate with other products and services.

--------------------------------------------------------------------------