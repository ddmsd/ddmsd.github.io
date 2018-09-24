---
title: "Asynchronous Python"
categories:
  - technical
tags:
  - Python
  - concurrency
---

The central focus of **Asyncio** is to perform multiple concurrent tasks that involve *waiting* period at the same time. The key insight for asynchronous programming is that while you wait for *this* task to finish, *other* tasks can execute.

## Threading vs Asynchronous
Due to the GIL(Global Interpreter Lock) in Python, only one thread is executed at any time, there is no multi-core parallel processing for both multi-threading and asynchronous programming. However, we can still scale up the I/O blocking tasks with the two programming styles.

For multi-threading programming, each thread is instantiated for one task. While one thread enters into the waiting phase, it is released and another thread starts to run. While for asynchronous programming, only one thread runs all the time, every time it starts to wait, it switch to the next task. In the latter case, you have one thread that *loops* over all different tasks.

The synchronization of different threads is one of the main difficulties in multi-threading programming. This is where the collision happens among different threads. With asynchronous programming, we can work around this by switching the tasks explicitly with Python *coroutine*. This is much safer.

Another advantage of asynchronous programming over multi-threading is the memory usage. Threads require a lot of memory, about 8MB per executing thread. This can consume a lot of memory when you run a thread per unique activity. While threads are costly to start, the cost of starting a generator coroutine is just a function call.
