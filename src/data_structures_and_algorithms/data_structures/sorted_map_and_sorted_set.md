# Sorted map and sorted set

## Overview

A sorted map and sorted set are abstract data types which extend the map and set by having their keys sorted according to their ordering.

On top of supporting the same operations of a map and a set ADT, a sorted map and a sorted set support the following extended operations:

| **Extended operation** | **Description**                                        |
| ---------------------- | ------------------------------------------------------ |
| `min()`                | Returns the smallest key in the sorted map.            |
| `max()`                | Returns the largest key in the sorted map.             |
| `successor(key)`       | Finds the key that immediately follows the given key.  |
| `predecessor(key)`     | Finds the key that immediately precedes the given key. |

## AVL tree

## Red-black tree

## In-memory B-tree

### Overview

According to *Introduction to Algorithms*, a B-Tree is a rooted tree with the following properties:

**Node**\
For some node `x`, it has the following attributes:
- `n`, the number of keys currently stored in node `x`
- `[key]`, an array of keys sorted in increasing order.
- `leaf`, a boolean value that is `true` if `x` is a leaf, and `false` if `x` is an internal node.
- `[child]`, an array of `x`'s child nodes

**Node and children count**\
For some node with \\(|keys|\\), then \\(|children| = |keys| + 1\\).

**Keys as seperators**\
The keys in the node separate the ranges of keys stored in its subtrees.

**Leaves and depth**\
All leaves have the same depth.

**Key count lower and upper bound**\
Every node has a lower and upper bound on the number of keys they can contain, which depends on a number \\(t \ge 2\\) called the minimum degree.

\\[
t - 1 \le |keys| \le 2t - 1
\\]

and so from the node and children count relationship defined above, then

\\[
t \le |children| \le 2t
\\]

However, the root node has no lower bound for the key count or children count, but rather that if the tree is nonempty, it must have at least one key.

<div class="warning">
<strong>Remark</strong>

We consider a node full when it has exactly \\(2t - 1\\) keys.
</div>

<div class="warning">
<strong>Remark</strong>

We can call a specific B-tree with some minimum degree \\(t\\) as "\\(t\\)-\\(2t\\)" tree, (e.g. a B-tree with minimum degree of \\(2\\) is called a \\(2\\)-\\(3\\)-\\(4\\) tree)
</div>

### Time complexity

| **Operation** | **Time complexity** |
| ------------- | ------------------- |
| Lookup        | \\(O(n)\\)         |
| Insertion     | \\(O(\log n)\\)    |
| Deletion      | \\(O(\log n)\\)    |

### Lookup

Beginning at the root node, the lookup procedure recurses as follows with the current node and target key as arguments: 
1. Linearly search through the keys in the current node. The search in the current node stops under one of two conditions:
    - Case 1: A key in the current node is found within some \\(i\\) satisfying \\(0 \le i \le |keys| - 1\\) such that it is greater than or equal to the target key.
    - Case 2: All the keys in the current node have been checked, and no key was found that is greater than or equal to the target key.
2. Once the search terminates, we proceed depending on the cases in step 2: 
    - Case 1: We now check if the key at index \\(i\\) is exactly equal to the target key. If it's equal, the the lookup was successful and we return the node and the index \\(i\\). Otherwise, (i.e. it was strictly greater than the target key), the algorithm must proceed to search deeper in the tree. 
    - Case 2: This means the all the keys in the current node is smaller than the target key. In this case, the algorithm must also search deeper in the tree.
3. If the linear search was unsuccessful, and the current node is not a leaf node, then we proceed to recurse on the child node at index \\(i\\). Otherwise, if the current node is a leaf node, it means there are no more possible keys to check, and hence, it must be that the key is not in the B-Tree, so we return `nil`.

### Insertion

1. Start from the root node. If it's full, that is, it contains \\(2t - 1\\) keys, where \\(t\\) is the minimum degree, create new root and set the old root as its child node. 

<div class="warning">
<strong>Remark</strong>

Insertion occurs only at the leaf nodes.
</div>

### Deletion

<div class="warning">
<strong>Remark</strong>

Unlike insertion, deletion can occur at any node — not just at the leaves.
</div>
