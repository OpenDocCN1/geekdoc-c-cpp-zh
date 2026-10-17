# 9.8. BINARY TREES

Earlier in this session, you have stumbled upon different means of storing elements and also the various means of representing the elements, their prominent features and also their shortcomings. Presented to you now is yet another concept of representing elements. The binary tree.

Before discussing the binary tree you have to understand what a tree is. A tree with reference to the data structures is similar to a hierarchical representation of an organization. In an organization you have a director right on top with a selected few managers as his lieutenants who have a number of superiors with a union of workers reporting to them. In 6th 5th 4th 3rd 2nd 1st 6th 5th 4th 3rd 2nd 1st Insertion Deletion, Deletion (Figure 9.6).

![](bbox=[0.342, 0.376, 0.665, 0.519])

**Figure 9.6.** Binary tree.

The similar way on the top of the tree is the root which consists of individual elements called the nodes. The nodes which evolve from this root are called the children and every child node in the tree has only one parent.

The root is an exception, which has no parent. The number of children that a node can accommodate depends on the type of the tree. In this section the type of tree that will be under focus will be the binary tree which is a fairly uncomplicated yet pretty powerful.

The reason that it is undemanding and simple can be attributed to the fact that it has a branching factor of only two. That is to say, any parent node can give birth to only two child nodes. A binary tree is a hierarchical representation of nodes with each node giving rise to two nodes. The different levels of hierarchy in the trees can be termed as the siblings, descendants, and ancestors. The siblings of a node are the other nodes of the parent whereas the descendants are the rest of the nodes that follow a particular node. The ancestors of a node are all the nodes that fall in between the path of the root and the node.