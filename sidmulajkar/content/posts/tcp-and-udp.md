---
title: "TCP and UDP - Simple yet Confusing🤔"
categories: [tcp, udp, networking, protocols, backend, developement, sidsblog]
tags: [tcp, udp, networking, protocols, backend, developement, ssidsblog]
date: 2021-10-02T17:26:04+05:30
description: "Best tutorial to understand the building blocks TCP & UDP to know which one to use"
author: Siddhant Mulajkar
draft: false
---


### TCP and UDP


A simple open-ended question that can test your whole sort of knowledge.

-------------------------------------------------------------------------------

###### What will be addressed in this post?

```
- The problem with packets (IP)
- TCP pros and cons
- TCP communication sample code

- UDP pros and cons
- UDP communication sample code

- Some questions based on them
```

-------------------------------------------------------------------------------

To start, I was asked a question in an interview, 

**What to use UDP or TCP in Building a Backend Application?**

I was like why only these 2 protocols, there are many others, like HTTP, HTTP2, XMPP, GRPC, QUIC

Why?

These two are the block fundamentals on which the other protocols work.

So, once when we understand the TCP and UDP, we can determine which other protocols to use.
```
For eg, UDP over TCP, then QUIC over HTTP
```

-------------------------------------------------------------------------------

Highly recommend just know about the OSI Model before getting on to the TCP and UDP.

**OSI is a model that standardized communication in the computer system, its what the internet runs on.**

![OSI Model](/images/tcpudp/osi.png)

-------------------------------------------------------------------------------

**The problem with the packets:**

The Internet Protocol (IP) describes how to split messages into multiple IP packets and route packets to their destination by hopping from router to router.


IP does not handle all the consequences of packets, however. For example:

```
- Packets can arrive out of order
- Packets can be corrupted
- Packets can be lost due to problems
- Similarly, packets might be duplicated
```

Fortunately, there are higher-level protocols in the Internet protocol stack that can deal with these problems.

Internet applications can choose the data transport protocol that makes the most sense for their application.

-------------------------------------------------------------------------------

TCP and UDP are the layer 4 protocols, i.e Transport Layer Protocols

The transport layer is the fourth layer in the open system interconnection (OSI) model and is responsible for end-to-end communication over a network.

![Transport Layer](/images/tcpudp/layer4.png)

It provides logical communication between application processes running on different hosts within a layered architecture of protocols and other network modules.

This layer is also responsible for the management of error correction, providing quality and reliability to the user.

-------------------------------------------------------------------------------

### Transmission Control Protocol (TCP)

The TCP is a transport protocol that is used on top of IP to ensure reliable transmission of packets. It is a connection-oriented protocol.

TCP includes mechanisms to solve many of the problems that arise from packet-based messaging, such as lost packets, out of order packets, duplicate packets, and corrupted packets.

Since TCP is the protocol used most commonly on top of IP, the Internet protocol stack is sometimes referred to as TCP/IP.

Packet Format 

When sending packets using TCP/IP, the data portion of each IP packet is formatted as a TCP segment.

![TCP](/images/tcpudp/tcpsegment.png)

When two computers want to send data to each other over TCP, they first need to establish a connection using a three-way handshake. 


![TCP](/images/tcpudp/3wayhanshake.png)

-------------------------------------------------------------------------------

TCP/IP Model vs OSI Model

![TCP vs OSI](/images/tcpudp/tcpvsosi.jpg)

-------------------------------------------------------------------------------

### TCP Pros:

```
- Acknowledgement
- Guaranteed Delivery
- Connection based(can be pro and con as well)
- Congestion Control
- Packet ordering and ack 
- Error Control Mechanism
```

Some follow up questions can be

- As you mentioned congestion control can you explain more about TCP Slow start. How do you see it?

- What is Tunneling? Can you explain in detail?

- Have you heard about SCTP Protocol. What is it?


-------------------------------------------------------------------------------

### TCP Cons:

```
- Larger Packets
- More Bandwidth
- Slower than UDP
- Stateful (whole new thing to mention about)
- Server memory (hogs up server memory)
```

Some follow up questions can be

- Can you explain to me Stateful vs Stateless protocols?

- Okay, then is DOS Attack possible on TCP? How?

- How does this affect the connections limit on the server?



-------------------------------------------------------------------------------

### User Datagram Protocol (UDP)

The UDP is a lightweight data transport protocol that works on top of IP.

UDP is simple but fast, at least in comparison to other protocols that work over IP. 


**What Kind Of Services Rely On UDP?**

It's often used for time-sensitive applications (such as real-time video streaming) where speed is more important than accuracy.


UDP provides a mechanism to detect corrupt data in packets, but it does not attempt to solve other problems that arise with packets, such as lost or out-of-order packets. That's why UDP is sometimes known as the Unreliable Data Protocol.


-------------------------------------------------------------------------------

##### UDP Cons:

```
- No Acknowledgement
- No Guaranteed Delivery
- Connectionless
- No Congestion Control
- No ordered Packets
- Security
```

##### UDP Pros:

```
- Smaller Packets
- Less bandwidth
- Faster than TCP
- Stateless
```

Some follow up questions:

- How is UDP used in DDoS attacks?

- What is RPC? Can you explain it in a bit more detail?
https://bit.ly/3Azn0ez

-------------------------------------------------------------------------------

[UDP Client-Server Implementation](https://www.geeksforgeeks.org/udp-server-client-implementation-c/)

Follow the link

**or**

With this code we will be implementing UDP Simple connection using Nodejs and netcat. Create a file udp.js

```
const dgram = require('dgram');
const socket = dgram.createSocket('udp4');

socket.on('message', (msg, rinfo) => {
  console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
});

socket.bind(8081);
```

Run the code or Start Debugging from your IDE and also open terminal and type in this command, to start the 2 way communication.

```
echo "foo" | nc -w1 -u 127.0.0.1 41234
```
-------------------------------------------------------------------------------

[TCP  Client-Server Implementation](https://www.geeksforgeeks.org/tcp-server-client-implementation-in-c/)

Follow the link

**or**

With this code we will be implementing TCP Simple connection using Nodejs and Telnet. Create a file tcp.js

```
const net = require("net")

const server = net.createServer(socket => {
    socket.write("Hello.")
    socket.on("data", data => {
        console.log(data.toString())
    })
})

server.listen(8080)
```

Run the code or Start Debugging from your IDE and also open terminal and type in this command, to start the 2 way communication similar to udp.

```
telnet 127.0.0.1 8080
```

-------------------------------------------------------------------------------

**If you think this is interesting, follow me on [twitter](https://twitter.com/sidmulajkar) and [linkedin](https://www.linkedin.com/in/siddhant-mulajkar/) for more content like this.**

-------------------------------------------------------------------------------
