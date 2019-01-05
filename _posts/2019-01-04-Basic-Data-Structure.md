---
title: "Basic Data Structure: Sequence"
categories:
  - technical
tags:
  - programming
  - algorithm
  - Python
---

# Array
Array is a contiguous block of memory. For an array `A`, retrieving and updating `A[i]` takes O(1) time. Python list is implemented as dynamic array that supports a _resize_ operation to handle operations like _insert_ and _append_. The resize operation increases the capacity of the array, that is, when we create a list of size __N__, Python allocate in fact __M__ items where M > N to provide extra room for future appends.(ref. _High Performance Python_)

As we _append_ data, we first use the extra room M - N. At N == M, we need to create a _new_ list with extra space, and we copy the old data into the new space.

_Deleting_ an element from an array entails moving all successive elements one over to the left to fill the vacancy. Same for inserting an element at the position _i_, the time complexity is O(n - i).

The array has the advantage that we can operate easily on both ends unlike linked-list.

## Tuple
Python tuples are static and immutable arrays that cannot be modified.

A tuple uses fewer resources as it does not need extra headrooms for resizing, for the same number of elements, a tuple takes the exact number of elements worth of memory while a list need more memory for headrooms. A list always takes larger memory than a tuple with the same data.

Another advantage of tuple is that for tuples of small size, the memory they use are not garbage collected in the background by Python. This make it fast to create tuples of small size since they can avoid communication with the operating system.

As __memory allocation is not cheap__, reusing space that has already been allocated can give performance speedup. For the same reason, it is also expensive to frequently resize a list with append operation, if append can not be avoided, it is better to use [collections.deque](https://docs.python.org/3.7/library/collections.html#collections.deque). The latter supports approximately O(1) performance for append and pop in either direction.


# Linked List
A _single linked list_ is a data structure that contains a sequence of nodes such that each node contain an object and a reference to the next node in the list.

For both linked-list and array, they contain object in a linear order. The key difference is that _deleting_ and _inserting_ an element in a linked list takes O(1) time complexity in comparison with O(n) in the worst case for arrays. The lookup takes O(n) time complexity for both.


# Stack and Queue
A stack is a data structure that supports last-in, first-out (LIFO), like the food you put in the refrigerator, whereas queues are first-in, first-out (FIFO), same as a waiting queue in a supermarket.



