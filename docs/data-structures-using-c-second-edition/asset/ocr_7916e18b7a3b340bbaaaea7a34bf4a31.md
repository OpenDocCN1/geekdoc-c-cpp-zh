# Example 11.6 Consider the B+ tree of order 4 given below and delete node 15 from it.

![](bbox=[0.205, 0.14, 0.795, 0.5])

Figure 11.13 Deleting node 15 from the given B+ Tree

**Note** Insertion and deletion operations are recursive in nature and can cascade up or down the B+-tree, thereby affecting its shape dramatically.

# 11.4 2-3 TREES

In the last chapter, we have seen that for binary search trees the average-case time for operations like search/insert/delete is o(log N) and the worst-case time is o(N) where N is the number of nodes in the tree. However, a balanced tree that has height o(log N) always guarantees O(log N) time for all three methods. Typical examples of height balanced trees include AVL trees, red-black trees, B trees, and 2-3 trees. We have already discussed these data structures in the earlier chapter and section; now we will discuss 2-3 trees.

+   - In a 2-3 tree, each interior node has either two or three children.
+   - Nodes with two children are called 2-nodes. The 2-nodes have one data value and two children
+   - Nodes with three children are called 3-nodes. The 3-nodes have two data values and three children (left child, middle child, and a right child)

This means that a 2-3 tree is not a binary tree. In this tree, all the leaf nodes are at the same level (bottom level). Look at Fig. 11.14 which shows a 2-3 tree.

![](bbox=[0.205, 0.825, 0.795, 0.905])

Figure 11.14 2-3 Tree