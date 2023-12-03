---
title: "B/B+ Trees How they are helpful in Database?"
categories: [btrees, bplus-trees, trees, data-structure, database, sidsblog]
tags: [btrees, bplus-trees, trees, data-structure, database, sidsblog]
date: 2021-10-25T17:26:04+05:30
description: "This tutorial will clear all your doubts regarding the B/B+ Trees and do you actually need it"
author: Siddhant Mulajkar
draft: false
---


##### What are those? Ever used trees while searching through the dataset.

**How B trees are useful in databases?**

---

To understand stuff more clearly let's take a scenario:

--

***Like we have a table, a huge table(millions of rows to go through), and we want to search to a particular numbered row by some id mentioned "100035" and not only pulling a row but getting most out of the pulled row.***

--

##### For the longest time, what we do is search the table one by one sequentially (page by page).

It's basically like a full table scan and if the key is also **not unique** we have to scan the whole table anyway, **which is very slow.**

--

##### How to make it faster? How do we make searching one million stuff faster?

Well,

- Split the table in like n numbers and parallelly process the database in a distributed manner. (Complicated but one way of doing it)

- Partition the database based on chunk key sizes.

- Indexing

---

**We always reduced the search space. That's it!**

So how do we use these trees and are they really useful? Best video to understand the concept by Abdul Bari

[![B Trees](/images/btrees/btree3.jpeg)](https://cf.piped.video/watch?v=aZjYr87r1b8 "B Trees")

---

#### Before going in-depth let's understand what B Tree is.

B-tree is a special type of self-balancing search tree in which each node can contain more than one key and can have more than two children. It is a generalized form of the binary search tree.


![B Tree](/images/btrees/btree.jpeg)

It is also known as a height-balanced m-way tree.

![B Tree](/images/btrees/btree1.jpeg)

---

### Why do you need a B-tree data structure?

- The need for B-tree arose with the rise in the need for lesser time in accessing the physical storage media like a hard disk. The secondary storage devices are slower with a larger capacity. 


- There was a need for such types of data structures that minimize disk access.

- Other data structures such as a binary search tree, AVL tree, red-black tree, etc can store only one key in one node.


- If you have to store a large number of keys, then the height of such trees becomes very large and the access time increases.

However, B-tree can store many keys in a single node and can have multiple child nodes. This decreases the height significantly allowing faster disk accesses.

---


##### Best site to create and learn B Trees visually with animations.

https://www.cs.usfca.edu/~galles/visualization/BTree.html

![B Tree Sample](/images/btrees/btree2.jpeg)

---


##### B Tree's Application:
--

B tree is used to index the data and provides fast access to the actual data stored on the disks since access to the value stored in a large database that is stored on a disk is a very time-consuming process.

--

The **major drawback** of the B-tree is the difficulty of traversing the keys sequentially. To understand more clearly,

If I wanted to search 1,3,5 at the same time from the above the Btree image. How do I do that?

- Ok let's find 1 first, then 3, ok then 5, which means we did 3 I/Os for finding 5.

- What if we're searching 100 items at the same time?

That's where **B+ Trees** comes in to picture...

---

##### B+ Tree:

***A B+ tree is an advanced form of a self-balancing tree in which all the values are present at the leaf level.***

![B+ Tree Sample](/images/btrees/bplus.png)

A B+ tree is an extension of a B tree which makes the search, insert and delete operations more efficient. We know that B trees allow both the data pointers and the key values in internal nodes as well as leaf nodes, this certainly becomes a drawback for B trees as the ability to insert the nodes at a particular level is decreased thus increase the node levels in it, which is certainly of no good. 


B+ trees reduce this drawback by simply **storing the data pointers at the leaf node level** and only storing the key values in the internal nodes. It should also be noted that the nodes at the leaf level are linked with each other, hence making the traversal of the data pointers easy and more efficient.

B+ trees come in handy when we want to store a **large amount of data** in the main memory. Since we know that the size of the main memory is not that large, so make use of the B+ trees, whose internal nodes that store the key(to access the records) are stored in the main memory whereas, the leaf nodes that contain the data pointers are actually stored in the secondary memory

---

##### Best site to create and learn B+ Trees visually with animations.

https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html

![B Plus Tree Sample](/images/btrees/bplus2.jpeg)

---

**Why B+ Tree?**

- B+ trees store the records which later can be fetched in an equal number of disk accesses.

- The height of the B+ tree remains balanced and very less as when compared to B trees even if the number of records stored in them is the same.


- Having fewer levels makes the accessing of records very easy.

- As the leaf nodes are connected like a linked list, we can easily search elements in sequential manners.


**Yeah, these are the concepts of B and B+ Trees.**

---

Almost, B trees are rarely used in the databases these days except some like MongoDB, **but have some value due to the simplicity and definitely have additional cost compared to the B+ tree.**


**We can use the B tree only when we want to search 1 value at a time and not multiples.**

But it's always **hard to fit** a B tree in memory fully compared to the B+ tree.

---

**The following are the differences between the B tree and B+ tree:**

No. | B Tree | B+ Tree |
--- | --- |--- |
1 | In the B tree, all the keys and records are stored in both internal as well as leaf nodes. | In the B+ tree, keys are the indexes stored in the internal nodes and records are stored in the leaf nodes.|
2 | In B tree, keys cannot be repeatedly stored, which means that there is no duplication of keys or records. | In the B+ tree, there can be redundancy in the occurrence of the keys. In this case, the records are stored in the leaf nodes, whereas the keys are stored in the internal nodes, so redundant keys can be present in the internal nodes. |
3 | In the Btree, leaf nodes are not linked to each other.| In B+ tree, the leaf nodes are linked to each other to provide the sequential access. |
4 | In Btree, searching is not very efficient because the records are either stored in leaf or internal nodes. | In B+ tree, searching is very efficient or quicker because all the records are stored in the leaf nodes. |
5 | Deletion of internal nodes is very slow and a time-consuming process as we need to consider the child of the deleted key also.	| Deletion in B+ tree is very fast because all the records are stored in the leaf nodes so we do not have to consider the child of the node. |
6 | In Btree, sequential access is not possible. | In the B+ tree, all the leaf nodes are connected to each other through a pointer, so sequential access is possible. |
7 | In Btree, the more number of splitting operations are performed due to which height increases compared to width. | B+ tree has more width as compared to height. |
8 | In Btree, each node has atleast two branches and each node contains some records, so we do not need to traverse till the leaf nodes to get the data. | In B+ tree, internal nodes contain only pointers and leaf nodes contain records. All the leaf nodes are at the same level, so we need to traverse till the leaf nodes to get the data. |
9 | The root node contains atleast 2 to m children where m is the order of the tree. | The root node contains atleast 2 to m children where m is the order of the tree. |

---

### Read More Blogs related to:

***[database]({{< relref "/tags/database/">}}) / [linuxsubsystem(wsl)]({{< relref "/tags/linuxsubsystem/">}}) / [flutter installation]({{< relref "/tags/flutter-installation">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberrypi">}})*** 

--