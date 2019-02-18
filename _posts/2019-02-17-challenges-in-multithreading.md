---
title: "Challenges in multi-threaded programs"
categories:          
  - technical
tags:
  - programming
toc: true
---
* **Races**: Two or more threads access the same address in memory and at least one of them writes to that address.
* **Starvation**: A processor needs a resource but never gets it.
* **Deadlock**: Thread A acquires Lock L1 and Thread B acquires Lock L2, folowing which A tries to acquire L2 and B tries to acquires L1.
* **Livelock**: A processor keeps retrying an operation that always fails.