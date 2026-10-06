# Selecting an Implementation 543

> Note: Comparing linear implementations of the ADT dictionary

+   - An unsorted array-based implementation of the ADT dictionary can efficiently insert an item at the end of an array. A removal, however, will require shifting data so that no gap remains in the array. Because the items are unsorted, retrieval will require a sequential search.
- A sorted array-based implementation requires shifting data during insertions and removals. Retrieval, however, can use an binary search because the items are sorted.
- An unsorted linked-based implementation can efficiently insert an item at the beginning of a linked chain. A removal will require a sequential search but no data shifts. Retrieval will also require a sequential search.
- A sorted linked-based implementation requires a sequential search but no data shifts during insertions and removals. Retrieval will also require a sequential search.

The nonlinear, binary search tree implementation of the ADT dictionary can be a better choice than a linear implementation, in general. If an n-node binary tree has minimum height—it has height $\lceil\log(n+1)\rceil$—the binary search tree implementation of the ADT dictionary certainly succeeds where linear implementations fail. You, easily compare to that of a binary search, locate an item in the retrieval operation and the first steps of add and remove operations. In the linked-based implementation of the binary search tree permits dynamic allocation of nodes, so it can handle a dictionary whose size is unknown.

This implementation also performs the second step of the insertion and removal operations: The actual insertion or removal of a node requires only a few pointer changes—plus traversal to the successor if the node to be removed has two children—rather than the possible shifting of all the dictionary entries, as the array-based implementations require. The binary search tree therefore combines the best aspects of the two linear implementations, avoids their disadvantages.

As Chapter 18 shows, the height of a binary search tree detects the order in which you perform the add and remove operations occur in a normal order, the height of the binary search tree will be close to its minimum value. You need to watch for a possible increase in the tree's height, however, the decreasing decrease in performance. If you use a variation of the binary search tree that remains balanced—as the next chapter will describe—you can keep the height of the tree near, $\log n$.

Figure 18 summarizes the order of the insertion, removal, retrieval, and traversal operations for the dictionary implementations so far in this chapter.

# FIGURE 18-8 The average-case order of the ADT dictionary operations for various implementations

| Insertion | Removal | Retrieval | Traversal |
|---|---|---|--|
| Unsorted array-based | O(1) | O(n) | O(n) | O(n) |
| Unsorted linked-based | O(1) | O(n) | O(n) | O(n) |
| Sorted array-based | O(n) | O(n) | O(log n) | O(n) |
| Sorted linked-based | O(n) | O(n) | O(n) | O(n) |
| Binary search tree | O(log n) | O(log n) | O(log n) | O(n) |