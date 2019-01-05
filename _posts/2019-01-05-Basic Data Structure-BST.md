---
title: "Data Structure: Binary Search Tree"
categories:
  - technical
tags:
  - programming
  - algorithm
  - Python
toc: true
use_math: true
---
# BST
A Binary Search Tree (BST) is a binary tree in which the key stored at a node is greater than or equal to **all the keys** stored at the nodes of its left subtree and less than or equal to all the keys of its right subtree.

## Basic Operations
Key lookup, insertion and deletion all take time proportional to the height of the tree, which can be in the worst-case $O(n)$. However, for a height-balanced BST like Red-black tree, all these operations take $O(\log n)$.

As the min and max keys of a BST are respectively the leftmost leaf and the right most leaf, it takes time $O(h)$ to descend from the root to the leaves where $h$ is the height of the tree.

To iterate through all the elements of a BST in sorted order, we just need to do an _inorder_ traversal of the binary tree itself. As each element is processed once, this operation takes time $O(n)$.

## How to use BST
In practice, a BST can be used as a sorted hash table where the lookup takes time $O(\log n)$ for a library implementation. In python, the package [bintrees](https://pypi.org/project/bintrees/) provides Binary RedBlack- and AVL-Trees. Another package [sortedcontainers](http://www.grantjenks.com/docs/sortedcontainers/) implements the sorted data structure as a sorted list of sorted lists where the insertion and deletion takes time $O(\sqrt n)$ asymptotically.


# B-tree
A B-tree is a generalization of BST in that a node can have more than two children. They are balanced search trees designed to work well on disks or other secondary storage devices. They are similar to Red-Black trees but better at minimizing disk I/O operations, so many database systems use B-trees.

If a node of B-tree has `n` sorted keys, then it has `n + 1` children, the `i-th` key of the node serves as the separation point of the children `i` and `i + 1`.

![B-tree](./img/B-tree.svg)