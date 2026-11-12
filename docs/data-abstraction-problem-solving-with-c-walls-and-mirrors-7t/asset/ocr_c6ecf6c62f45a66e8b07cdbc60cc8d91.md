# # Heaps

+   Contents
+   17.1 The ADT Heap 503
+   17.2 An Array-Based Implementation of a Heap 506
+   17.2.1 Algorithms for the Array-Based Heap Operations 508
+   17.2.2 The Implementation 512
+   17.3 A Heap Implementation of the ADT Priority Queue 516
+   17.4 Heap Sort 519
+   Summary 522
+   Exercises 522
+   Programming Problems 523

+   Prerequisites
+   Chapter 13 Queues and Priority Queues
+   Chapter 15 Trees
+   Chapter 16 Tree Implementations

Chapter 15 introduced the ADTs binary tree and binary search tree. This chapter will present the ADT heap, which is a special kind of complete binary tree that provides an efficient implementation of the ADT priority queue. You can also use a heap to sort an array as efficiently as you can by using either a quick sort or a merge sort.

# ## 17.1 The ADT Heap

A heap is a complete binary tree that either is empty or whose root

A heap is a special complete binary tree

+   - Contains a value greater than or equal to the value in each of its children, and
+   - Has heaps as its subtrees