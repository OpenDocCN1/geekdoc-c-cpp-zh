+   A single root node

+   A root node connected by branches to one or more smaller trees

A node's level or depth is the distance from the node to the root. In particular, the root's level is 0.

A node's height is the length of the longest path from the node downward through the tree to a leaf node. In other words, it's the distance from the node to the bottom of the tree.

A tree's height is the same as the height of the root.

A subtree of tree T rooted at the node R is the node R and all its descendants. For example, in Figure 10-1 the subtree rooted at node 5 is the tree containing nodes 5, 6, 7, 8.

An ordered tree is one in which the order of the children is important. For example, many algorithms treat the left and right child in a binary tree different. An unordered tree is one in which the order of the children doesn't matter (Usually a tree has an ordering, even if it's not particularly important to the algorithm. This is true simply because the children or branches are stored in an array or some collection that imposes an ordering on them).

For any two nodes, the first common ancestor (or least common ancestor) might be one of the node is the ancestor of both nodes that is closest to them. Another way to think about this is to start at one node and move up toward the root until you reach the first node that is an ancestor of the other node. For example, in Figure 10-1 the first common ancestor of nodes 3 and 5 is node 4.

Note that the first common ancestor of two nodes might be one of the nodes. For example, in Figure 10-1 the first common ancestor of nodes 5 and 6 is node 5.

Note also there is a unique path between any two nodes in a tree that doesn't cross any node more than once. The path starts at the first node, moves up to the nodes' first common ancestor, and then moves the tree to the second node.

A full tree is one in which every node has either zero or as many children as the tree's degree. For example, in a binary, every node has either zero or two children. The tree shown in Figure 10-1 is not full because node 5 has only one child.

A complete tree is one in which every level is completely full, except the bottom level, where all the nodes are pushed to the left as possible. Figure 10-2 shows a complete binary tree. Notice that this tree is not full because the third node on level 2 has only one child.

A perfect tree is full, and all the leaves are at the same level. In other words, the tree holds every possible node for a tree of its height.

Figure 10-3 shows examples of full, complete, and perfect binary trees.