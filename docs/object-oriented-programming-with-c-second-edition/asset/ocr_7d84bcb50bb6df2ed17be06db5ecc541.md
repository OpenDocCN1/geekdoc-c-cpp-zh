# Object-Oriented Programming with C++

The ‘My Programs’ folder has two folders beneath it—C Language’ and ‘C++’. The ‘C++’ folder has three folders beneath it—Data Structures’, ‘Calculator Proj’, and ‘Tic Tac Proj.

Suppose this folder structure is represented by a data structure, in which each folder is represented by a node. It is obvious that each node will contain, from the name of the folder, one or more pointers to other similar nodes. Such a data structure is called a tree. Trees can be created in C++ in order to model these real-world tree-like structures.

# 9.5.1 Binary Trees

A binary tree is a tree in which each node is linked to a maximum of two nodes. Let us look at a simplified figure of a binary tree (Figure 9.58). In this figure, the nodes have been represented by circles. Each node has been labelled with a different alphabet. The links between nodes have been represented with straight lines.

The tree has been drawn in a top-down fashion. This means that A is the root node. The figure will be described in greater detail shortly.

![](bbox=[0.223, 0.403, 0.853, 0.633])

Figure 9.58 A binary tree

A binary tree is a finite set of elements. It is either empty or partitioned into three disjoint subsets. The first subset contains only one element, which is the root of the tree. The other subsets are themselves binary trees. One of them is considered to be the left sub-tree and the other one is considered to be the right sub-tree. Either or both of the sub-trees can be empty.

Let us understand this with the help of the example shown in Figure 9.58. There are nine nodes in the tree depicted above. The root node is labelled ‘A’. The tree has a left sub-tree and a right sub-tree. The root node of the left sub-tree is labelled ‘B’ whereas the root of the right sub-tree is labelled ‘C’

Let us use this description further. The sub-tree is also a tree. The root node is ‘B’. The node labelled ‘D’ is the root node of the left sub-tree of ‘B’ and the node is the root of the right sub-tree of ‘D’ does not have a left or right sub-tree. The tree starting from ‘E’ has a left sub-tree only.

A node that does not have children is known as leaf. Thus, in the above figure, ‘D’, ‘G’, ‘H’, and ‘I’ are leaves.