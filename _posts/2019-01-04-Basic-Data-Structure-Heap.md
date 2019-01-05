---
title: "Basic Data Structure: Heap"
categories:
  - technical
tags:
  - programming
  - algorithm
  - Python
toc: true
---

# Heap
Heaps are a simple data structure that supports priority queue operations like _insert_ and _extract_min_. They work by maintaining the partial order on a set of elements that are weaker than the sorted order. Heaps are usually implemented as a _complete binary tree_ that for each node, its key is less or equal than the keys of its children.

**Definition.** A complete binary tree is a binary tree in which every level, except the last, is completely filled. For the last level, all the nodes are as far left as possible.
{: .notice--info}

For a heap of height $h$, it can be implemented with an array of $2^h - 1$ elements. Suppose that the first element's index is `1`, for a node at the position `i`, its left and right children are respectively `2 * i` and `2 * i + 1`, and its parent is `i // 2`. Therefore for a heap `h`, we have `h[i] <= h[2 * i + 1] and h[i] <= h[2 * i + 2]`, where the first index is 0 in most programming languages.

The implementation of heap in Python is [heapq](https://docs.python.org/3.7/library/heapq.html?highlight=heapq#module-heapq), it only provides min-heap functionality.

## Insertion
When inserting a new element in a heap of size n, the new element is placed at the left-most open spot in the heap array. We then _bubble up_ the new element by comparing its key with the key of its parent till it arrives at an appropriate position. The time complexity of the insertion is O(log n).

## Extract the min
The min of a heap `h` is the element `h[0]`, `h[0]` returns the min key of the heap without popping it. To extract the min, we can use `heapq.heappop(h)`. As this operation leaves the position 0 empty, we can fill it by moving the `(n - 1)th` element to position 0. After that, the dissatisfied element is _bubbled down_ by swapping the root with the min child recursively till the root is less or equal than both children. The extract min operation also has the time complexity O(log n).

## Sort
A *heapsort* is a sorting algorithm. We first construct a heap by inserting the new element into the heap one by one, next we extract the min element from the heap till it's empty. It runs in worst case O($n\log n$) and is an inplace sort.

Another advantage of heapsort is that you can efficiently insert new elements into the heap during the sort, provided that the newly inserted element is greater or equal than the last extracted min key. This is useful for task schedulers in operating systems for example.