---
title: "Basic Data Structure: Hash Table"
categories:          
  - technical
tags:
  - programming
  - algorithm
  - Python
toc: true
use_math: true
---
Hash table is a data structure used to store keys, or keys with corresponding values that supports insert, delete and lookup operations with $O(1)$ *on average*. However, for lookup, the expected time is $O(n / m)$ where $m$ is the size of hash table and for the worst case it can take $O(n)$ with a lot of collisions.

# Hashing
A _hash function_ $H$ is a mathematical function that maps keys to integers, usually a big integer. A hash table is an array of $m$ slots, for a string $S$ for example, the slot it will take in the hash table is $\floor*{H(S) / m}$.

A hash function should guarantee that equal keys have equal hash code, and a _good_ hash function should also "spread" keys in the hash table in order to decrease the number of collisions, this is not easy in practice.