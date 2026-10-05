# 5.3.3 Array Implementation for Complete Binary Trees

The previous section points out that a large fraction of the space in a typical binary tree node implementation is devoted to overhead, not to storing data. This section presents a simple, compact implementation for complete binary trees. Recall that binary trees have all levels except the bottom filled completely and the bottom level has all its nodes filled from left to right. Thus, a complete binary tree of $n$ nodes has only one shape. You might think that a complete binary tree is such an unusual occurrence that there is no reason to develop a special implementation for it. However, the complete binary tree is the most important being the heap data structure discussed in Section 5.5. Heaps are often used to implement priority queues (Section 5.5) and for external sorting algorithms (Section 8.5.2).

We begin by assigning numbers to the node positions in the complete binary tree, level by level, from left to right as shown in Figure 5.12(a). An array can store the tree's values efficiently, placing each data value in the array position corresponding to that node's position within the tree. Figure 5.12(b) lists the indices for the children, parent, and siblings of each node in Figure 5.12(a). From 5.12(b), you see a pattern regarding the positions of a node's relatives within the array. Simple formulas can be derived for calculating the array index for each relative of a node $r$ from $r$'s index. No explicit pointers are necessary to reach a node's left or right child. This means there is no overhead to the array implementation if the array is selected to be size $n$ for a tree of $n$ nodes.

The formula for calculating the array index of the relatives of a node $r$ are as follows. The total number of nodes in the tree is $n$. The index of the node in question is $r$, which may fall in the range 0 to $n-1$.

+   * Parent($r$) = $(r-1)/2$ if $r \neq 0$.
* Left child($r$) = $2r+1$ if $2r+1 < n$.
* Right child($r$) = $2r+2$ if $2r+2 < n$.
* Left sibling($r$) = $r-1$ if $r$ is even.
* Right sibling($r$) = $r+1$ if $r$ is odd and $r+1 < n$.

# 5.4 Binary Search Trees

Section 4.4 presented the dictionary ADT, along with dictionary implementations based on sorted and unordered lists. When implementing the dictionary with an unordered list, inserting a new record into the dictionary can be performed quickly by putting it at the end of the list. However, searching an unordered list for a particular record requires $\Theta(n)$ time in the average case. For a large database, this is probably too slow. Alternatively, the records can be stored in a sorted list. If the list is implemented using a linked list, then no speedup to the search operation will