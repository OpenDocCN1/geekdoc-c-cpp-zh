# # Trees and Binary Trees

In the previous chapters, linear data structures such as arrays, stacks and queues have been studied. Trees and graphs are two dimensional in structure and are referred to as non-linear data structures. The study of non-linear data structures is considered in this and forth-coming chapters. This chapter particularly deals with defining the tree data structure, the terminology related to them and their representation in different ways. A basic type of tree, i.e. binary tree is discussed in detail with its representation, operations and traversals. This chapter also include threaded binary trees, ADT of binary trees, changing a general tree into a binary tree along with a detailed explanation about expression trees as an application.

# ## 9.1 INTRODUCTION

A tree is a finite set of one or more nodes. In this set of nodes a node is referred to as a root. The other nodes could be partitioned into T1, T2, T3 ... Tt, disjoint sets of trees where t >= 0, and are referred to as subtrees of the tree.

Every node in a tree represents a unit of information. The links/arcs between the nodes are known as branches and specify the association between the units of information. A tree is depicted in Figure 9.1.

All nodes are reachable from the root through a unique sequence of branches called a path, and no node is left isolated in the tree. The number of arcs in a path is called the length of the path.

By definition (1) connected less and (2) acyclicity or no closed loops are ensured in a tree. The tree structure does not allow any set of nodes to link together to from a closed loop or to be acyclic.

# ## 9.2 TERMINOLOGIES

The number of branches associated with a node is called the degree of a node. A branch that comes to the node is the indegree branch and the branch that emerges from the node is the outdegree branch. Degree of a node is the sum of indegree and outdegree branches. A node whose indegree is zero is called the root. Nodes whose outdegree is zero is the leaf nodes or terminal nodes. The degree of a tree is the maximum degree of the node in the tree. All the nodes other than root and leaf nodes are the internal nodes or non-terminal nodes. All the