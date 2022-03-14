---
title: "How to Handle the Double booking problem in an app or website just using the database? "
categories: [factors, double-booking problem, concurrency control, lock mechanism, time stamping, pessimistic approach, optimistic approach, database, sidsblog]
tags: [factors, double-booking problem, concurrency control, lock mechanism, time stamping, pessimistic approach, optimistic approach, database, sidsblog]
date: 2022-03-13T17:26:04+05:30
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

In this blog, I want to purely talk from the perspective of handling a situation like this, **just considering the database itself.**

---

Before getting into the details of the problem we need to first understand the concepts of 

```
- Concurrency Control
- Lock Mechanisms &
- Time Stamping
```

### **Concurrency Control**

It is a procedure in DBMS which helps us for the management of two simultaneous processes to execute without conflicts between each other, these conflicts occur in multi-user systems.

Concurrency can simply be said to be executing multiple transactions at a time. It is required to increase time efficiency. If many transactions try to access the same data, then inconsistency arises. Concurrency control is required to maintain consistent data.

**The simultaneous execution of transactions over shared databases can create several data integrity and consistency problems.**

These protocols are categorized as:

- Lock Based Concurrency Control Protocol
- Time Stamp Concurrency Control Protocol
- Validation Based Concurrency Control Protocol

### **Locking**

Lock guarantees exclusive use of data items to a current transaction. It first accesses the data items by acquiring a lock, after completion of the transaction it releases the lock.

Types of Locks

The types of locks are as follows −

- Shared Lock [Transaction can read only the data item values]
- Exclusive Lock [Used for both read and write data item values]

### **Time Stamping**

The timestamp is a unique identifier created by DBMS that indicates the relative starting time of a transaction. Whatever transaction we are doing is stored from starting time of the transaction and denotes a specific time.

This can be generated using a system clock or logical counter. This can be started whenever a transaction is started. Here, the logical counter is incremented after a new timestamp has been assigned.

---

### For simpler understanding,

There are two approaches to this situation for maintaining the concurrency

1. Pessimistic Concurrency Control -
    
    Let’s say it’s cloudy outside and might probably rain, so I decided to take the umbrella with me today whether it rains or not.
    
2. Optimistic Concurrency Control -
    
    Let’s say it’s cloudy outside and might probably rain, but I decide to not take the umbrella with me, and let’s see when it rains at that moment.
    
    (referenced from hussain nasser {Backend Engineering with HN})    

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

Double booking at the same time can create some race conditions for this situation so we can probably use 2-phase locking or strict 2-phase, 3 phase-locking mechanisms to ensure that the consistency is maintained. (pessimistic approach)

but locking is expensive to keep the table in the memory while updating the table using the lock.

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

**Well the Answer is :**

It totally depends, on what use, we are using the concurrency model for using the specific database to avoid this problem.