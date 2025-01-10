# Priority queue

## Overview

A priority queue is an abstract data type where elements are assigned priorities, such those with higher priorities are served before those with lower priorities.

| **Operation**  | **Description**                                                                  |
| -------------- | -------------------------------------------------------------------------------- |
| `size()`       | Returns the number of elements in the priority queue.                            |
| `is_empty()`   | Returns whether the priority queue is empty or not                               |
| `top()`        | Returns the element with the top priority without removing it.                   |
| `add(element)` | Adds an element to the priority queue.                                           |
| `remove_top()` | Removes and returns the element with the highest priority in the priority queue. |

## Binary Heap

### Overview

**Definition**\
A binary heap is a complete binary tree with one of the heap ordering properties:
- The min-heap property: the value of each parent node is less than or equal to the value of its two child nodes.
- The max-heap property: the value of each parent node is greater than or equal to the value of its two child nodes.

Hence, the minimum-value element is at the root for a min-heap, and the maximum-value element is at the root for a max-heap.

**Array layout**\
Heaps are commonly laid out as arrays, where nodes are placed based on Eytzinger's method:
- The root is always at index \\(1\\) 
- For some node at index \\(i\\):
    - the left child is located at index \\(2i\\)
    - the right child is located at index \\(2i + 1\\)
    - its parent node is located at \\(\lfloor \frac{i}{2} \rfloor\\)

### Time complexity

| **Operation** | **Time complexity** |
| ------------- | ------------------- |
| Build heap    | \\(O(n)\\)         |
| Lookup        | \\(O(1)\\)         |
| Insertion     | \\(O(\log n)\\)    |
| Deletion      | \\(O(\log n)\\)    |

### Node sifting mechanisms

Many heap operations make use of sifting mechanisms, called "sift up" and "sift down" to place nodes in their correct position within the tree.

**Sift up**\
For some node, we repeatly "sift" the node "up" if the node's key is less than its parent's key (min-heap) or if the node's key is greater than its parent's key (max-heap) by swapping positions with its parent.

**Sift down**\
For some node, we repeatly "sift" the node "down" when its key is greater than one of its children's key by swapping it with the smallest children (min-heap) or when its key is less than one of its children's key by swapping it with the largest children (max-heap).

### Build a heap from initial elements

To build a heap from initial elements of a list in \\(O(n)\\) worst case time, we build in a bottom-up manner as follows:
1. Copy over all elements in the original list into the backing dynamic array which has the first element at index \\(0\\) as `nil`.
1. Beginning at the parent of the last element in the list, up to and including index \\(1\\), then, repeatedly call sift down.

### Lookup

Return the element at index \\(1\\).

### Insertion

1. Add an element as the righmost leaf of the heap (i.e. the last element in the backing array).
2. Sift up the node containing the element to correct its position within the tree.

### Deletion

1. Set the root node's key to be the same key of the last node in the heap.
2. Remove the last node in the heap now that we've placed its key in the root node.

