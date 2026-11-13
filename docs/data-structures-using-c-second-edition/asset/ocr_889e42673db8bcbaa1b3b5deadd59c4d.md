external nodes in the left sub-tree and the right sub-tree. However if the tree is empty, that is TREE = NULL, then the number of external nodes will be zero. But if there is only one node in the tree, then the number of external nodes will be one.

```
Number of external nodes = totalExternalNodes(left sub-tree) +
totalExternalNodes (right sub-tree)
```

Consider the tree given in Fig. 10.18. The total number of external nodes in the given tree can be calculated as:

+   Total external nodes of left sub-tree = 1
+   Total external nodes of left sub-tree = 2
+   Total external nodes = 1 + 2 = 3

![](bbox=[0.1, 0.3, 0.56, 0.5])

Figure 10.21 shows a recursive algorithm to calculate the total number of external nodes in a binary search tree. For every node, we recursively call the algorithm on its left sub-tree as well as the right sub-tree. The total number of external nodes at a given node is then returned by adding the external nodes in its left as well as right sub-tree. However if the tree is empty, that is TREE = NULL, then the number of external nodes will be zero. Also if there is only one node in the tree, then there will be only one external node (that is the root node).

# 10.2.6 Finding the Mirror Image of a Binary Search Tree

Mirror image of a binary search tree is obtained by interchanging the left sub-tree with the right sub-tree at every node of the tree. For example, given a tree T, the mirror image of T can be obtained as T'. Consider the tree T given in Fig. 10.22.

![](bbox=[0.1, 0.56, 0.3, 0.7])

Figure 10.23 shows a recursive algorithm to obtain the mirror image of a binary search tree. In the algorithm, if TREE = NULL, that is if the current node in the tree has one or more nodes, then the algorithm is recursively called at every node in the tree to swap the nodes in its left and right sub-trees.

![](bbox=[0.1, 0.73, 0.46, 0.92])

# 10.2.7 Deleting a Binary Search Tree

To delete/remove an entire binary search tree from the memory, we first delete the elements/nodes in the left sub-tree and then delete the nodes in the right sub-tree. The algorithm shown in Fig. 10.24 gives a recursive procedure to remove the binary search tree.

# 10.2.8 Finding the Smallest Node in a Binary Search Tree

The very basic property of the binary search tree states that the smaller value will occur in the left sub-tree. If