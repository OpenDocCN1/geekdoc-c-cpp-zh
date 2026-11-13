# # CHAPTER 12 Heaps

> ### LEARNING OBJECTIVE
> A heap is a specialized tree-based data structure. There are several variants of heaps which are the prototypical implementations of priority queues. We have already discussed priority queues in Chapter 8. Heaps are also crucial in several efficient graph algorithms. In this chapter, we will discuss three types of heaps—binary heaps, binomial heaps, and Fibonacci heaps.

# ## 12.1 BINARY HEAPS

A binary heap is a complete binary tree in which every node satisfies the heap property which states that:

```
IF B is a child of A, then key(A) ≥ key(B)
```

This implies that elements at every node will be either greater than or equal to the element at its left and right child. Thus, the root node has the highest key value in the heap. Such a heap is commonly known as a max-heap.

![](bbox=[0.09, 0.76, 0.55, 0.9])

Figure 12.1 Binary heaps

Alternatively, elements at every node will be either less than or equal to the element at its left and right child. Thus, the root has the lowest key value. Such a heap is called a min-heap.

Figure 12.1 shows a binary min heap and a binary max heap. The properties of binary heaps are given as follows:

+   * Since a heap is defined as a complete binary tree, all its elements can be stored