# 12.3.1 Operations on Heaps

The basic operations on heaps are listed as follows:

+   1. Create—creates an empty heap to which the root points
+   2. Insert—inserts an element into the heap
+   3. Delete—deletes max (or min) element from the heap
+   4. ReheapUp—rebuilds the heap when we use the insert() function
+   5. ReheapDown—rebuilds the heap when we use the delete() function

A heap is generally not traversed, searched, or printed. To implement the insert and delete operations, we need two other operations: reheapUp and reheapDown. The advanced operations include merge, which merges two heaps.

# ReheapUp

If we have a nearly complete binary tree with n elements, the first n – 1 elements satisfy the order property of heaps, but the last element does not. That is, the structure would be a heap if the last element was not there. The reheapUp operation repairs the structure so that it is a heap by lifting the last element up the tree until that element reaches a proper position in the tree. This restructuring can be graphically viewed in Fig. 12.11.

![](bbox=[0.245, 0.475, 0.855, 0.64])

Fig. 12.11 ReheapUp operation

We can note that in Fig. 12.11 the last node in the heap was out of order. After the reheap, it is in its correct location, and the heap has been extended by one node.

As a heap is a complete or nearly complete tree, the node must be placed in the last leaf level at the first leftmost empty position as in Fig. 12.11. If the new node’s key is larger than its parent, it is lifted up the tree by exchanging the child and parent keys and the data. The data eventually moves to the correct position in the heap by repeatedly exchanging child–parent keys and data. In brief, reheapUp repairs a broken heap by lifting the last element up the tree until it reaches the correct location in the heap.

![](bbox=[0.68, 0.75, 0.905, 0.88])

Fig. 12.12 General heap structure

Figure 12.12 shows a general heap structure.

Let us consider an example.