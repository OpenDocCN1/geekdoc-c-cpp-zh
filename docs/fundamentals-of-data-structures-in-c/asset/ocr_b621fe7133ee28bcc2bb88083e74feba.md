![](bbox=[0.31, 0.07, 0.78, 0.2])

![](bbox=[0.31, 0.21, 0.78, 0.33])

![](bbox=[0.31, 0.34, 0.78, 0.46])

![](bbox=[0.31, 0.47, 0.78, 0.63])

Fig. 4.16 : Steps for insertion operation in a binary search tree.

# Deletion of a Node

Another primitive operation that can be done in a binary search tree is the deletion of a node. Memory is to be released for the node to be deleted. A node can be deleted from the tree from three different places namely,

+   * Deleting the leaf node
+   * Deleting the node with only one child
+   * Deleting the node with two children.

# Deleting the leaf node

Steps followed to delete a leaf node from the binary search tree.

+   * Search the parent of the leaf node, and make the link to the leaf node as NULL.
+   * Release the memory for the deleted node.