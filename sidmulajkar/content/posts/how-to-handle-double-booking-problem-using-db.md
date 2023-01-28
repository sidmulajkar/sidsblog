---
title: "How to Handle the Double booking problem in an app or website just using the database? "
categories: [factors, double-booking problem, concurrency control, lock mechanism, time stamping, pessimistic approach, optimistic approach, database, kubernetes, microservices, sidsblog]
tags: [factors, double-booking problem, concurrency control, lock mechanism, time stamping, pessimistic approach, optimistic approach, database, kubernetes, microservices, sidsblog]
date: 2022-03-19T17:26:04+05:30
description: "In this blog, I just want to purely talk from the perspective of handling a situation like this, just considering the database itself."
author: Siddhant Mulajkar
draft: false
---


How to Handle the Double booking problem in an app or website just using the database?


**Well the Answer is :**

It totally depends, on what use, we are using the concurrency model for using the specific database to avoid this problem.

---

#### Firstly, what the heck is double booking problem?

An online movie ticket booking system provides its customers with the ability to book movie tickets online. BookMyShow as an example allows the customers to browse movies currently being running in a city and to book seats, anywhere anytime for a show. **What if two or more people book the ticket for a specific seat of the specific movie for the same movie theatre.**

or 

Simply a train booking system/app which allows travelers to book tickets of the trains anywhere anytime for travel. What if ...

**Two passengers are allotted the same berth of the same train** for the same travel date.

![Double Booking](/images/doublebookingdb/doublebook1.png)

---

**Now how do we handle this situation as a database/backend engineer?**

```go
I am not talking about designing a similar system like this.
```

In this blog, I want to ***purely talk from the perspective of handling a situation like this, just considering the database itself.***

---

### For simpler understanding,

There are two approaches to this situation for maintaining the concurrency

1. **Pessimistic Concurrency Control -**
    
    Let’s say it’s cloudy outside and might probably rain, so I decided to take the umbrella with me today whether it rains or not.
    
2. **Optimistic Concurrency Control -**
    
    Let’s say it’s cloudy outside and might probably rain, but I decide to not take the umbrella with me, and let’s see when it rains at that moment.
    
    (referenced from hussain nasser {Backend Engineering with HN})    

---

***Before getting into the details of the problem we need to first understand the concepts of***

```
- Concurrency Control
- Lock Mechanisms &
- Time Stamping
```

1. ### **Concurrency Control**

It is a procedure in DBMS which helps us for the management of two simultaneous processes to execute without conflicts between each other, these conflicts occur in multi-user systems.

Concurrency can simply be said to be executing multiple transactions at a time. It is required to increase time efficiency. If many transactions try to access the same data, then inconsistency arises. Concurrency control is required to maintain consistent data.

**The simultaneous execution of transactions over shared databases can create several data integrity and consistency problems.**

These protocols are categorized as:

- Lock Based Concurrency Control Protocol
- Time Stamp Concurrency Control Protocol
- Validation Based Concurrency Control Protocol

2. ### **Locking**

Lock guarantees exclusive use of data items to a current transaction. It first accesses the data items by acquiring a lock, after completion of the transaction it releases the lock.

The types of locks are −

- **Shared Lock** [Transaction can read only the data item values]
- **Exclusive Lock** [Used for both read and write data item values]

3. ### **Time Stamping**

The timestamp is a unique identifier created by DBMS that indicates the relative starting time of a transaction. Whatever transaction we are doing is stored from starting time of the transaction and denotes a specific time.

This can be generated using a system clock or logical counter. This can be started whenever a transaction is started. Here, the logical counter is incremented after a new timestamp has been assigned.

---

#### Lets say in

1. Pessimistic Concurrency Control - 
    
    Users want to write the data at the same time then it will access the write permission to the single user based on some queue preference and create an **exclusive lock** for it to avoid the other users to access and update the data {based on the values changed}. 
    
    **This can create congestions for the operations required to be executed by the DB and making wait other transactions is similar to making people wait which would not create the best user experience for the users**, but the exclusive lock will make sure that the data present in the database, when read by other users, will be up to date. 
    
    The locks are generally present for some milliseconds if the transaction is successful, or some minutes if no transaction is done, essential kept active for some period of time for specific user. If transaction is successful, it won’t make other transactions wait for access, but for more real-time user experience it is not that good compared to the optimistic one but **more reliable for sure.**

2. Optimistic Concurrency Control - 
    
    It is based on the assumption that conflict is rare and it is more efficient to allow transactions to proceed without imposing delays to ensure serializability.
    
    The users want to write the data at the same time then they will be given the access permission to write (for multiple users) based on some access preference and update the data {on the value changed based on transactions}.
    
    **If both the users update the data at the same time then it will be just garbage data which will be of no use, as this type of concurrency control is not having any concepts of locks in it.**
    

---
But here the main implementation is done using the concept called **time to check to time to use (using the timestamp and validation based control protocols):**

---


Let’s explain this in more detail here, **if the users are granted to read the data at the same time then before transacting or updating the data from users we need to check for update, if it is updated then we need to abort the transaction or simply update the current change and show not available.**

---

### Problems with the Pessimistic Approach:

Double booking at the same time can create some race conditions for this situation so we can probably use ***2-phase locking or strict 2-phase, 3 phase-locking mechanisms to ensure that the consistency is maintained. (pessimistic approach)***

--

***but locking is expensive to keep the table in the memory while updating the table using the lock.***

--

**Multiple locks can be used like row level, table level, etc and most databases don’t allow row-level locking because if one transaction updates the whole rows, and other thousands of columns in the table then keeping them in memory is not efficient and cost-effective.**

Link to read more on Locks: [https://www.javatpoint.com/dbms-lock-based-protocol](https://www.javatpoint.com/dbms-lock-based-protocol)

[https://www.tutorialspoint.com/distributed_dbms/distributed_dbms_commit_protocols.htm](https://www.tutorialspoint.com/distributed_dbms/distributed_dbms_commit_protocols.htm)

---

### Problems with the Optimistic Approach:

The problems which arises while using concurrency are as follows −

- **Updates will be lost** − One transaction does some change and another transaction deletes that change. One transaction nullifies the updates of another transaction.

    ![Update Lost](/images/doublebookingdb/updatelost.png)

    Two transactions T1 and T2 read, modify, write to the same data item in an interleaved fashion for which an incorrect value is stored in x. T2 reads the value of X before T1 changes, hence the updated value resulting from T1 is lost or the final value of x is 15, which is incorrect.

- **Uncommitted Dependency or dirty read problem** − As the variable has updated in one transaction, at the same time another transaction has started and deleted the value of the variable there, the variable is not getting updated or committed that has been done on the first transaction this gives us false values or the previous values of the variables, this is a major problem.

    ![Dirty Read](/images/doublebookingdb/dirtyread.png)
    
    T2 reads the updated value of X made by T1, but T1 fails and rolls back. So, T2 reads an incorrect value of X.


- **Inconsistent retrievals**− One transaction is updating multiple different variables, another transaction is in the process to update those variables, and the problem that occurs is the inconsistency of the same variable in different instances.

    ![Inconstient Retrievals](/images/doublebookingdb/incosistentretrival.png)    
    T1 consists of two parts – subtract 5 from X and add 5 to Y.
    In T2, the value of X is updated but the value of Y is not updated. The sum variable stores an incorrect value.

    Ref Link:  [https://www.tutorialspoint.com/explain-the-main-problems-in-concurrency-control-dbms](https://www.tutorialspoint.com/explain-the-main-problems-in-concurrency-control-dbms)

---

### Well the Answer is :

***It totally depends, on what use, we are using the concurrency model for using the specific database to avoid this problem.***

2PC, 3PC, MVCC, SAGA are some of the patterns through which we control concurrency but,

--

**ACID is mostly depended on the Isolation of the Transactions.**

As we know that, in order to maintain consistency in a database, it follows **ACID properties**. Among these four properties (Atomicity, Consistency, Isolation, and Durability) **Isolation determines how transaction integrity is visible to other users and systems.**

It means that a transaction should take place in a system in such a way that it is the only transaction that is accessing the resources in a database system. 
Isolation levels define the degree to which a transaction must be isolated from the data modifications made by any other transaction in the database system. A transaction isolation level is defined by the following phenomena – 

 

1. **Dirty Read** – A Dirty read is a situation when a transaction reads data that has not yet been committed. For example, Let’s say transaction 1 updates a row and leaves it uncommitted, meanwhile, Transaction 2 reads the updated row. If transaction 1 rolls back the change, transaction 2 will have read data that is considered never to have existed.

2. **Non Repeatable read** – Non Repeatable read occurs when a transaction reads the same row twice and gets a different value each time. For example, suppose transaction T1 reads data. Due to concurrency, another transaction T2 updates the same data and commit, Now if transaction T1 rereads the same data, it will retrieve a different value.

3. **Phantom Read** – Phantom Read occurs when two same queries are executed, but the rows retrieved by the two, are different. For example, suppose transaction T1 retrieves a set of rows that satisfy some search criteria. Now, Transaction T2 generates some new rows that match the search criteria for transaction T1. If transaction T1 re-executes the statement that reads the rows, it gets a different set of rows this time.

--

Based on these phenomena, The **SQL standard defines** four isolation levels : 

1. **Read Uncommitted** – Read Uncommitted is the lowest isolation level. In this level, one transaction may read not yet committed changes made by other transactions, thereby allowing dirty reads. At this level, transactions are not isolated from each other.

2. **Read Committed** – This isolation level guarantees that any data read is committed at the moment it is read. Thus it does not allow dirty read. The transaction holds a read or write lock on the current row, and thus prevents other transactions from reading, updating, or deleting it.

3. **Repeatable Read** – This is the most restrictive isolation level. The transaction holds read locks on all rows it references and writes locks on referenced rows for update and delete actions. Since other transactions cannot read, update or delete these rows, consequently it avoids non-repeatable read.

4. **Serializable** – This is the highest isolation level. A serializable execution is guaranteed to be serializable. Serializable execution is defined to be an execution of operations in which concurrently executing transactions appears to be serially executing.


![Transaction Isolation](/images/doublebookingdb/transactnLevel.png)

---

Another great blog on **Distributed transaction patterns for microservices compared** by **Bilgin Ibryam(Red-Hat-PM)** 

https://developers.redhat.com/articles/2021/09/21/distributed-transaction-patterns-microservices-compared

---

Here's a Video on Concurrency Control in Postgress:

[![Postgress Conference](/images/doublebookingdb/postgresscon.jpeg)](https://cf.piped.video/watch?v=ZxhBkBNxvR0 "Postgress Conference")

---

Learned about a **"Commercial SQL DB"** which is designed for scale:
https://www.cockroachlabs.com/

**FAQ-Link:** 

https://www.cockroachlabs.com/docs/stable/frequently-asked-questions.html

![Cockroach DB](/images/doublebookingdb/cockroachdb.jpeg)

---