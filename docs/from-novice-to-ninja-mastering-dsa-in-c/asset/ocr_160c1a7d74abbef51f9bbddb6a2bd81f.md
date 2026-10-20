# Chapter 6: Trees and Graphs

# Binary Trees and Binary Search Trees: Foundations of Tree Structures

# Understanding Binary Trees:

A binary tree is a hierarchical data structure composed of nodes, each having at most two children, referred to as the left child and the right child. The topmost node is known as the root, and nodes with no children are called leaves. Binary trees are fundamental in computer science and serve as the building blocks for more complex tree structures.

# Anatomy of a Binary Tree:

![](bbox=[0.05, 0.26, 0.94, 0.4])

In the above example, 5 is the root, with 3 and 8 as its left and right children, respectively. Node 3 has children 1 and 4.

# Binary Search Trees (BST):

A Binary Search Tree is a specific type of binary tree where the left child of a node contains values less than the node, and the right child contains values greater than the node. This ordering property enables efficient search, insertion, and deletion operations.

# Example of Binary Search Tree:

![](bbox=[0.05, 0.54, 0.94, 0.68])

In this BST, for any given node, all nodes in its left subtree have values less than the node, and all nodes in its right subtree have values greater than the node.

# Operations on Binary Search Trees:

+   > **Search**: Starting from the root, compare the target value with each node and traverse left or right accordingly until finding the target or reaching a leaf.
+   > **Insertion**: Search for the correct position to insert the new node based on the ordering property of the BST.
+   > **Deletion**: Locate the node to be deleted and handle cases based on the number of children:-