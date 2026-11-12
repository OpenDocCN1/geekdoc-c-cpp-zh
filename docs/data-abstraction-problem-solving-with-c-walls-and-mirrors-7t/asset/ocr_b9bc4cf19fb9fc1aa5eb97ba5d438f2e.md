A heap is similar to a binary search tree, although it differs from a binary search tree in two significant ways:

+   * While you can view a binary search tree as sorted, a heap is ordered in a much weaker sense.
+   * While binary search trees come in many different shapes, heaps are always complete binary trees.

In our definition of a heap, the root contains the item with the largest value. Such a heap is also known as a **maxheap**. A **minheap**, on the other hand, places the item with the smallest value in its root. An example of a maxheap and a minheap are given in Figure 17-1. Exercises 1 and 8 and Programming Problem 3 consider the minheap further.

# FIGURE 17-1 (a) A maxheap and (b) a minheap

![](bbox=[0.25, 0.28, 0.9, 0.43])

The ADT heap has the following operations:

> **Note: ADT heap operations**
> * Test whether a heap is empty
> * Get the number of nodes in a heap
> * Get the height of a heap
> * Get the item in the heap
> * Get the item in the heap's root
> * Insert a new item into the heap
> * Remove the item in the heap's root
> * Remove all nodes from the heap
> 
> Depending on whether the heap is a maxheap or a minheap, the removal and retrieval operations respectively involve either the largest or the smallest item in the heap

# FIGURE 17-2 UML diagram for the class Heap

| Heap |
| --- |
| +isEmpty(): boolean |
| +getNumberOfNodes(): integer |
| +getHeight(): integer |
| +peekTop(): ItemType |
| +add(newData: ItemType): boolean |
| +remove(): boolean |
| +clear(): void |