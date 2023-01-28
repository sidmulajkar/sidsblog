---
title: "What is TCP Slow Start?"
categories: [tcp, slowstart, congestion-control, mechanism, sidsblog]
tags: [tcp, slowstart, congestion-control, mechanism, sidsblog]
date: 2021-10-02T17:26:04+05:30
description: "This tutorial will clear all your doubts regarding the TCP Slow Start and is it really a problem"
author: Siddhant Mulajkar
draft: false
---

### Does it affect Web Application Performance?

Yes, it's a feature, not an issue but can be a problem sometimes while analyzing and designing the app.

![TCP Slow Start](/images/tcpslowstart/tcp1.png)

---

**TCP slow start is a congestion-avoidance algorithm that balances the speed of a network connection.**

A slow start gradually increases the amount of data transmitted until it finds the network’s maximum carrying capacity.

One of the most common ways to optimize the speed of a connection (i.e. increase the amount of bandwidth). 

However, any link can become overloaded if a device tries to send out too much data. Oversaturating a link is known as congestion, and it can result in slow communications.

![TCP Slow Start](/images/tcpslowstart/tcp2.png)

---


### How TCP slow start works

TCP slow start is one of the first steps in the congestion control process. It balances the amount of data a sender can transmit (known as the congestion window) with the amount of data the receiver can accept (known as the receiver window). The lower of the two values becomes the maximum amount of data that the sender is allowed to transmit before receiving an acknowledgment from the receiver.

Step-by-step, here’s how slow start works:

- A sender attempts to communicate to a receiver. The sender’s initial packet contains a small congestion window, which is determined based on the sender’s maximum window.

- The receiver acknowledges the packet and responds with its own window size. If the receiver fails to respond, the sender knows not to continue sending data.

- After receiving the acknowledgement, the sender increases the next packet’s window size. The window size gradually increases until the receiver can no longer acknowledge each packet, or until either the sender or the receiver’s window limit is reached.


Once a limit has been determined, slow start’s job is done. Other congestion control algorithms take over to maintain the speed of the connection.

---


**Example:**

CDN providers often adjust their slow start window to maximize performance. 

The initial congestion window parameter (initcwnd) can have notable impact on the speed of network. 

When the receiver has sent fewer ack's to the sender, more data can be transmitted faster.


Most large CDN providers default to an initcwnd of 10, meaning the CDN will transmit 10 packets before requesting an acknowledgment. 

Tuning initcwnd for optimum performance can have a significant improvement in TCP performance.


[https://www.cdnplanet.com/blog/initcwnd-settings-major-cdn-providers/](https://www.cdnplanet.com/blog/initcwnd-settings-major-cdn-providers/)

---

### Benefits of TCP slow start:

1. Users experience uninterrupted connections 

2. Users also experience faster downloads 

3. Enterprises see less network congestion since slow start regulates bandwidth and prevents the sender from having to continuously retransmit data.

--

It is never the ideal condition that the transmission is seamless after the initial slow start, as there might be some errors introduced.

This unfavorable condition certainly depends heavily on a different system and network settings.


However, it is sufficient to indicate that there are insufficiencies in  the existing Slow-Start process. 


***With this understanding of the whole concept, it's like giving a cold start to your car before actually using it.***


That's why many of them have specially advised or recommended to warm up the TCP server with the proxies connected with the upstream server sending in some garbage requests.

--

So, whenever the new request comes in, we have the beautiful TCP connections running.

The TCP Handshake itself takes some time, which is reduced using TCP Fast Open(TFO). 

So opening & closing connections is also tedious as a Backend Engineer, not when using a browser.

![TCP Fast Open](/images/tcpslowstart/tcpfastopen.jpg)

---

### That's why eager loading is always preferred over lazy loading the TCP Connections.


***This can be very evidently found in Serverless computing that has been provided by Cloud Services like AWS, Azure, GCP.***


We can't do much about the TCP Slow Start, as we need it so that we don't flood the network with the requests. 

Without the congestion control algorithms, the internet will just be down as we might lose the packets, retransmission, performance issues, etc.

--

Read a paper, regarding the same, named as 

**Problems and Solutions for the TCP Slow start process. By University of Toronto**

[https://tinyurl.com/2h7hssbf](https://tinyurl.com/2h7hssbf)

**Another Article:**

Building Blocks of TCP [https://tinyurl.com/2h7hssbf](https://hpbn.co/building-blocks-of-tcp/)

---

### Conclusion

So next time while designing the app and using a networking protocol like TCP, do analyze the whole process and then develop the thing.