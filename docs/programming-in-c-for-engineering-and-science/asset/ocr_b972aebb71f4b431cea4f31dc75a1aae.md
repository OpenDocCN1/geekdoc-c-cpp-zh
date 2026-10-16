For the next step, one of the two sublists, the left half or the right half, must be searched and both must therefore be accessible from this node. This is possible if we maintain two links, one to each of these sublists. Because these sublists are searched in the same manner, these links should refer to nodes containing the middle elements in these sublists:

![](bbox=[0.24, 0.24, 0.74, 0.32])

By the same reasoning, in the next step, links from each of these “second-level” nodes are needed to access the middle elements in their sublists:

![](bbox=[0.24, 0.44, 0.73, 0.52])

The resulting structure is easier to visualize if we “stretch it out” into two dimensions so that it has a treelike shape:

![](bbox=[0.28, 0.64, 0.72, 0.78])

This structure is called a binary search tree and is a special kind of binary tree, which is a special instance of a more general structure called a tree.

# 16.4.1 Tree Terminology and Examples

A tree consists of a finite collection of nodes linked together in such a way that if the tree is not empty, then one of the nodes, called the root, has no incoming links, but every other node in the tree can be reached from the root by following a unique sequence of consecutive links.

Trees derive their names from the treelike diagrams that are used to picture them. For example, the diagram on the next page shows a tree having nine vertices in which the node labeled 1 is the root. As this diagram indicates, trees are usually drawn upside down, with the root at the top and the leaves—nodes with no outgoing links—at the bottom. Nodes that are directly accessible from a given node (by using only one link) are called the children of that node, and a node is said to be the parent of its children. For example, in the following tree, node 3 is the parent of nodes 5, 6, and 7, and these nodes are the children of node 3 and are called siblings.