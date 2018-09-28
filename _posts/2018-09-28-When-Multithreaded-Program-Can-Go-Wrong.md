---
title: "When Multithreaded Program Can Go Wrong"
categories:
  - technical
tags:
  - threading
  - concurrency
---
There are three common ways that multithreaded programs can go wrong

- race condition
- memory visibility
- deadlock

# Race Condition

This happens when two of more threads try to modify one variable in the program. As many languages implement the operation like `+=` with a pattern *read-modify-put*, when we want to increment a variable twice with two threads, instead of executing the order one by one, they can copy the same original value to a temporary location and increment it by one then copy it back. In this case, we will only have one incrementation instead of two.


# Memory visibility

The [Java memory model](http://www.cs.umd.edu/~pugh/java/memoryModel/) defines when changes to memory made by one thread become visible to another thread. The bottom line is that there are no guarantees unless both the reading and the writing threads use synchronization.

For example, when one thread modifies a variable and another reads the value of it. If *both* threads are not synchronized, there's no guarantee that the thread can ever read the modified value.


# deadlock

When you have more than one lock in a multithreaded program, your threads may become *deadlocked*. The solution for this is always acquire locks in a fixed global order.
