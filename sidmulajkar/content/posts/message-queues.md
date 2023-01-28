---
title: "Message Queues! What are those and when to use them? "
categories: [queue, data-structure, database,backend-engineering, sidsblog]
tags: [queue, data-structure, database,backend-engineering, sidsblog]
date: 2021-11-26T17:26:04+05:30
description: "This tutorial will help you understand the message queues."
author: Siddhant Mulajkar
draft: false
---

**Message queues ...📨 📨**


**The role of message queuing in a micro-service architecture.**

--


##### *When is the right time to use a message queue and why is a database rarely the best tool for a queue-based problem?*

A blog on backend engineering...

![Message Queues](/images/messagequeue/messagequeue1.png)

--------------------------------------------------------------------------


Imagine that we have a web application for customers to upload a text document, which then converts it into a PDF, and then emails it back to the customer. 

This site receives a lot of PDF creation requests every second and every request takes a second to process. 


An orderly, organized queue is needed to be able to handle all requests in a timely manner.

--

**USER SCENARIO**
1. Customer uploads a text document
2. Your application converts the text document into a PDF
3. Your application emails the PDF back to the customer

![Message Queues Scenario](/images/messagequeue/messagequeue2.png)

--------------------------------------------------------------------------

**Message queuing makes it possible for applications to communicate asynchronously, by sending messages to each other via a queue.**

--------------------------------------------------------------------------

Using a message queue is ***highly recommended when we need to process a high-volume of asynchronous messages.***

A message queue is perfect to use when we want a high performance, highly concurrent and scalable system that can process thousands of messages per second concurrently across many servers/processes.

--------------------------------------------------------------------------

What is **Synchronous vs Asynchronous Communication?**

![Communication](/images/messagequeue/messagequeue3.png)

--------------------------------------------------------------------------

A message queue provides temporary storage between the sender and the receiver so that the sender can keep operating without interruption when the destination program is busy or not connected.

Asynchronous processing allows a task to call a service, and move on to the next task.

--

##### Message queue use cases:

Now we might think, “where on earth would a message queue fit in my architecture”? 

The simple and quick answer is when:

- we have “timeout errors” due to too many requests at the same time.

- we need a decoupled way to communicate between or within your application.

- we are polling a data store too often and we want this data store to be available to answer qualified queries instead

- we need to scale up and down during peak hours

--------------------------------------------------------------------------

##### Message queues can also be used for more advanced scenarios like

- Images Scaling
- Sending large/many emails
- Search engine indexing
- File scanning
- Video encoding
- Delivering notifications
- PDF processing

--------------------------------------------------------------------------

##### Main features and benefits of message queuing

- There are no direct connections between programs.

- Communication between programs can be independent of time.

- Work can be carried out by small, self-contained programs.

- Communication can be driven by events.

- Applications can assign a priority to a message.

- Security.

- Data integrity.

- Recovery support.

--------------------------------------------------------------------------


##### The role of message queuing in a micro-service architecture:

In a microservice architecture, there are different functionalities divided across different services, that offer various functionalities. 

These services are coupled together to form a complete software application.

![Micro Service Architecture](/images/messagequeue/messagequeue4.png)


Typically, in a micro-service architecture, there are cross-dependencies, which entail that no single service can perform its functionalities without getting help from other services. 


This is where the system must have a mechanism in place which allows services to keep in touch with each other without getting blocked by responses.


Message queuing fulfills this purpose by providing a means for services to push messages to a queue asynchronously and ensure that they get delivered to the correct destination.


***To implement a message queue between services, you need a message broker, think of it as a mailman, who takes mail from a sender and delivers it to the correct destination.***

--------------------------------------------------------------------------

##### Okay, this seems great, but what if we need the same message to be processed by two or more microservices? Well, there are different types of message queues:

A message queue can be point-to-point, where there is only one queue and one consumer

![Point to Point](/images/messagequeue/messagequeue8.png)


Alternatively, a message queue can use a **Publisher-Subscriber** format, where a Publisher (Producer) sends a message to a queue (in this case called a Topic), and all the Subscribers receive a copy of the message that can be retained or not.

![Pub Sub Model](/images/messagequeue/messagequeue7.png)


--------------------------------------------------------------------------

The queue can provide protection from service outages and failures.

##### Examples of queues: Kafka, Heron, real-time streaming, Amazon SQS, and RabbitMQ.