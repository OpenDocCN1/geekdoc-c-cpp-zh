```
Height (TREE)
Step 1: IF TREE == NULL
Return 0
ELSE
SET LeftHeight = Height(TREE -> LEFT)
SET RightHeight = Height(TREE -> RIGHT)
IF LeftHeight > RightHeight
Return LeftHeight + 1
ELSE
Return RightHeight + 1
[END OF IF]
[END OF IF]
Step 2: END
```

# Figure 10.17 Algorithm to determine the height of a binary search tree

![](bbox=[0.102, 0.355, 0.252, 0.475])

# Figure 10.18 Binary search tree

```
totalNodes(TREE)
Step 1: IF TREE == NULL
Return 0
ELSE
Return totalNodes(TREE -> LEFT) +
totalNodes(TREE -> RIGHT) + 1
[END OF IF]
Step 2: END
```

# Figure 10.19 Algorithm to calculate the number of nodes in a binary search tree

```
totalInternalNodes(TREE)
Step 1: IF TREE == NULL
Return 0
[END OF IF]
IF TREE -> LEFT == NULL AND TREE -> RIGHT == NULL
Return 0
ELSE
Return totalInternalNodes(TREE -> LEFT) +
totalInternalNodes(TREE -> RIGHT) + 1
[END OF IF]
Step 2: END
```

# Figure 10.20 Algorithm to calculate the total number of internal nodes in a binary search tree

in the tree, we count the number of nodes in the left sub-tree and the right sub-tree.

Number of nodes = totalNodes(left sub-tree) + totalNodes(right sub-tree) + 1

Consider the tree given in Fig. 10.18. The total number of nodes in the tree can be calculated as:
Total nodes of left sub-tree = 1
Total nodes of right sub-tree = 5
Total nodes of tree = (1 + 5) + 1
= 7

Figure 10.19 shows a recursive algorithm to calculate the number of nodes in a binary search tree. For every node, we recursively call the algorithm for its left sub-tree as well as the right sub-tree. The total number of nodes at a given node is then returned by adding 1 to the number of nodes in its left as well as right sub-tree. However if the tree is empty, that is TREE == NULL, then the number of nodes will be zero.

# Determining the Number of Internal Nodes

To calculate the total number of internal nodes or non-leaf nodes, we count the number of internal nodes in the left sub-tree and the right sub-tree and add 1 to it for the root node).

Number of internal nodes = totalInternalNodes(left sub-tree) + totalInternalNodes(right sub-tree) + 1

Consider the tree given in Fig. 10.18. The total number of internal nodes in the tree can be calculated as:
Total internal nodes of left sub-tree = 0
Total internal nodes of right sub-tree = 3
Total internal nodes of tree = (0 + 3) + 1
= 4

Figure 10.20 shows a recursive algorithm to calculate the total number of internal nodes in a binary search tree. For every node, we recursively call the algorithm on its left sub-tree as well as the right sub-tree. The total number of internal nodes at a given node is then returned by adding internal nodes in its left as well as right sub-tree. However, if the tree is empty, that is TREE == NULL, then the number of internal nodes will be zero. Also if there is only one node in the tree, then the number of internal nodes will be zero.

# Determining the Number of External Nodes

To calculate the total number of external nodes or leaf nodes, we add the number of