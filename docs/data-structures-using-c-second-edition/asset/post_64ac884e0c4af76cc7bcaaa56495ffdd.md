
Cascading-Cut takes O(1) time exclusive of recursive calls. Therefore, the actual cost of decrease-Val_Fib-Heap including all recursive calls is O(c).

### Example 12.10 Decrease the value of node 39 to 9 in the Fibonacci heap given below.

### Solution

![](img/be6359df08208122bec6fad1103de211_392_0.png)

Figure 12.38 Fibonacci heap

### Deleting a Node

A node from a Fibonacci heap can be very easily deleted in O(D(n)) amortized time. The procedure to delete a node is given in Fig. 12.39.

```
Del_Fib_Heap (H, x)
Step 1: DECREASE_VAL_FIB_HEAP(H, x, -∞)
Step 2: EXTRACT-MIN_FIB-HEAP(H)
Step 3: END
```

to delete a node is given in Fig. 12.39. Del_Fib_Heap assigns a minimum value to x. The node x is then removed from the Fibonacci heap by making a call to the Extract-Min_Fib-Heap procedure. The amortized time of the delete procedure is the sum of the O(1) amortized time of decrease-Val_Fib-Heap and the O(D(n)) amortized time of Extract-Min_Fib-Heap.

Figure 12.39 Algorithm to delete a node from a Fibonacci heap

## 12.4 COMPARISON OF BINARY, BINOMIAL, AND FIBONACCI HEAPS

Table 12.1 makes a comparison of the operations that are commonly performed on heaps.

Table 12.1 Comparison of binary, binomial, and Fibonacci heaps

| Operation | Description | Binary | Binomial | Fibonacci |
|---|---|---|---|---|
| Create Heap | Creates an empty heap | O(n) | O(n) | O(n) |
| Find Min | Finds the node with minimum value | O(1) | O(log n) | O(n) |
| Delete Min | Deletes the node with minimum value | O(log n) | O(log n) | O(log n) |
| Insert | Inserts a new node in the heap | O(log n) | O(log n) | O(1) |
| Decrease Value | Decreases the value of a node | O(log n) | O(log n) | O(1) |
| Union | Unites two heaps into one | O(n) | O(log n) | O(1) |

## 12.5 APPLICATIONS OF HEAPS

Heaps are preferred for applications that include:

- Heap sort It is one of the best sorting methods that has no quadratic worst-case scenarios. Heap sort algorithm is discussed in Chapter 14.
- Selection algorithms These algorithms are used to find the minimum and maximum values in linear or sub-linear time.
- Graph algorithms Heaps can be used as internal traversal data structures. This guarantees that runtime is reduced by an order of polynomial. Heaps are therefore used for implementing Prim's minimal spanning tree algorithm and Dijkstra's shortest path problem.

## POINTS TO REMEMBER

- A binary heap is defined as a complete binary tree in which every node satisfies the heap property. There are two types of binary heaps: max heap and min heap.
- In a min heap, elements at every node will either be less than or equal to the element at its left or right child. Similarly, in a max heap, elements at every node will either be greater than or equal to element at its left and right child.
- A binomial tree of order i has a root node whose children are the root nodes of binomial trees of order i–1, i–2, ..., 2, 1, 0.
- A binomial tree $B_i$ of height i has $2^i$ nodes.
- A binomial heap $H$ is a collection of binomial trees that satisfy the following properties: Every binomial tree in $H$ satisfies the minimum heap property. There can be one or zero binomial trees for each order including zero order.
- A Fibonacci heap is a collection of trees. Fibonacci heaps differ from binomial heaps, as they have a more relaxed structure, allowing improved asymptotic time bounds.

## EXERCISES

### Review Questions

- 1. Define a binary heap.
- 2. Differentiate between a min-heap and a max-heap.
- 3. Compare binary trees with binary heaps.
- 4. Explain the steps involved in inserting a new value in a binary heap with the help of a suitable example.
- 5. Explain the steps involved in deleting a value from a binary heap with the help of a suitable example.
- 6. Discuss the applications of binary heaps.
- 7. Form a binary max-heap and a min-heap from the following sequence of data: 50, 40, 35, 25, 27, 33.
- 8. Heaps are excellent data structures to implement priority queues. Justify this statement.
- 9. Define a binomial heap. Draw its structure.
- 10. Differentiate among binary, binomial, and Fibonacci heaps.
- 11. Explain the operations performed on a Fibonacci heap.
- 12. Why are Fibonacci heaps preferred over binary and binomial heaps?
- 13. Analyse the complexity of the algorithm to unite two binomial heaps.
- 14. The running time of the algorithm to find the minimum key in a binomial heap is O(log n). Comment.
- 15. Discuss the process of inserting a new node in a binomial heap. Explain with the help of an example.
- 16. The algorithm Min-Extract_Binomial-Heap() runs in O(log n) time where n is the number of nodes in H. Justify this statement.
- 17. Explain how an existing node is deleted from a binomial heap with the help of a relevant example.
- 18. Explain the process of inserting a new node in a Fibonacci heap.
- 19. Write down the algorithm to unite two Fibonacci heaps.
- 20. What is the procedure to extract the node with the minimum value from a Fibonacci heap? Give the algorithm and analyse its complexity.
- 21. Consider the figure given below and state whether it is a heap or not.

![](img/be6359df08208122bec6fad1103de211_394_0.png)

- 22. Reheap the following structure to make it a heap.

![](img/be6359df08208122bec6fad1103de211_394_1.png)

- 23. Show the array implementation of the following heap.

![](img/be6359df08208122bec6fad1103de211_394_2.png)

- 24. Given the following array structure, draw the heap.

| 45 | 27 | 36 | 18 | 16 | 21 | 23 | 10 |
|---|---|---|---|---|---|---|---|

Also, find out
(a) the parent of nodes 10, 21, and 23, and
(b) index of left and right child of node 23.

- 25. Which of the following sequences represents a binary heap?
(a) 40, 33, 35, 22, 12, 16, 5, 7
(b) 44, 37, 20, 22, 16, 32, 12
(c) 15, 15, 15, 15, 15, 15, 15

- 26. A heap solution is given as: 52, 32, 42, 22, 12, 27, 37, 12, 7. Which element will be deleted when the deletion algorithm is called thrice?

- 27. Show the resulting heap when values 35, 24, and 10 are added to the heap of the above question.

- 28. Draw a heap that is also a binary search tree.

- 29. Analyse the complexity of heapify algorithm.

- 30. Consider the Fibonacci heap given below and then decrease the value of node 33 to 9. Insert a new node with value 5 and finally delete node 19 from it.

![](img/be6359df08208122bec6fad1103de211_394_3.png)

### Multiple-choice Questions

- 1. The height of a binary heap with n nodes is equal to
(a) O(n) (b) O(log n)
(c) O(n log n) (d) O(n^2)

- 2. An element at position i in an array has its left child stored at position
(a) 2i (b) 2i + 1
(c) i/2 (d) i/2 + 1

- 3. In the worst case, how much time does it take to build a binary heap of n elements?
(a) O(n) (b) O(log n)
(c) O(n log n) (d) O(n^2)

- 4. The height of a binomial tree Bi, is
(a) 2i (b) 2i + 1
(c) i/2 (d) i

- 5. How many nodes does a binomial tree of order 0 have?
(a) 0 (b) 1
(c) 2 (d) 3

- 6. The running time of Link_Binomial_Tree() procedure is
(a) O(n) (b) O(log n)
(c) O(n log n) (d) O(1)

- 7. In a Fibonacci heap, how much time does it take to find the minimum node?
(a) O(n) (b) O(log n)
(c) O(n log n) (d) O(1)

### True or False

- 1. A binary heap is a complete binary tree.
- 2. In a min heap, the root node has the highest key value in the heap.
- 3. An element at position 1 has its parent stored at position 1/2.
- 4. All levels of a binary heap except the last level are completely filled.
- 5. In a min-heap, elements at every node will be greater than its left and right child.
- 6. A binomial tree B_r has 2^r nodes.
- 7. Binomial heaps are ordered.
- 8. Fibonacci heaps are rooted and ordered.
- 9. The running time of Min_Binomial_Heap() procedure is O(log n).
- 10. If there are m roots in the root lists of H1 and H2, then Merge_Binomial_Heap() runs in O(n log m) time.
- 11. Fibonacci heaps are preferred over binomial heaps.

### Fill in the Blanks

- 1. An element at position i in the array has its right child stored at position ____.
- 2. Heaps are used to implement ____.
- 3. Heaps are also known as ____.
- 4. In ____, elements at every node will either be less than or equal to the element at its left and right child.
- 5. An element is always deleted from the ____.
- 6. The height of a binomial tree B_r is ____.
- 7. A binomial heap is defined as ____.
- 8. A binomial tree B_r has ____ nodes.
- 9. A binomial heap is created in ____ time.
- 10. A Fibonacci heap is a ____.
- 11. In a Fibonacci heap, mark[x] indicates ____.
