Various topics discussed earlier in the book including Stacks, Queue, Link list would fall under the category of linear data structure. In linear data structure, items are arranged one after the other. During, accessing of item, traversal takes place by visiting all the nodes previously placed. Complexity, of linear data structure is O(n). Correspondingly, performance is the major bottleneck in linear data structure. To improve the performance, a new data structure known as tree is devised. Tree is an example of non-linear data structure. In non-linear data structure, data are arranged in parent-child relationship. Same has been

![](bbox=[0.16, 0.3, 0.85, 0.47])

demonstrated in the following figure.

Tree categorization is determined by the maximum number of child that any parent can accommodate at any point in time. However, a node may have less number of nodes than the maximum number of a node that it can accommodate. Trees are further defined based on their degree. For instance tree with degree ‘2’ is termed as binary, tree of degree ‘3’ is termed ternary, whereas the tree of degree ‘n’ is termed as n-ary tree. For this chapter, we have considered the binary tree only.

# 7.2 BASIC TERMINOLOGY

At any point in time, a tree may hold a number of nodes, which are arranged in parent and child relationship. The node from where tree originates that node is termed as root. Node after the root node is child of another node, this will continue till we do not reach at the leaf node. Each node is acting as child of other node (except the root node). Therefore, tree can be defined as non linear data structure, organized in parent child relationship. Each node is again acting as a tree.

Before discussing the tree, it is worth discussing some of the terms that will be frequently used throughout our discussion.

Siblings: Children of same parent are known as siblings. In the tree, illustrated in the figure 7.3, the two nodes with the values 5 and 40 are siblings, since both of them are children of the same parent i.e. node 20.

Non-terminal node: Nodes in a tree with at least one child are known as non-terminal node. It can also be defined as all the nodes other than the terminal nodes are termed as non-