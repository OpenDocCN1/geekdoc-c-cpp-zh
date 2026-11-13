Min heap: A min heap is a complete binary tree in which the value in each node is less than or equal to those in its children (if any). The tree in Figure 11.7 is a min heap.

![](bbox=[0.35, 0.14, 0.65, 0.3])

Figure 11.7 A min heap

Since a heap is a complete binary tree, a heap can be efficiently represented using a one-dimensional array. The array in Figure 11.9 corresponds to the min heap in Figure 11.8.

![](bbox=[0.3, 0.41, 0.7, 0.58])

Figure 11.8 A min heap

| | 15 | 23 | 18 | 26 | 33 | 21 | 70 | | |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

Figure 11.9 Array implementation of a complete binary tree given in Figure 11.8

For any element in array position i, the left child is in position 2i, the right child is in the cell after the left child (2i+1), and the parent is in position ⌊i/2⌋. Thus, using array links are not required and operations required to traverse the tree are extremely simple and are likely to be fast.

# 11.3.1 Priority Queue Interface

It is assumed that when two elements of type T are compared using relational operators such as < and <= the element priorities are compared. Unlike ADT specification for priority queue, the interface specification in Figure 11.10(a) is programming language dependent (C++).