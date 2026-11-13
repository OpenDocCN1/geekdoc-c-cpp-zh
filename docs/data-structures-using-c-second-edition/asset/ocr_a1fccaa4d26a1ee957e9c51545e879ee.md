Tree (a) is an AVL tree. In tree (b), a new node is inserted in the left sub-tree of the right sub-tree of the critical node a (node a is the critical node because it is the closest ancestor whose balance factor is not -1, 0, or 1), so we apply RL rotation as shown in tree (c). Note that the new node has now become a part of tree τ.

While rotation, node c becomes the root, with a and b as its left and right children. Node a has τ1 and τ3 as its left and right sub-trees and τr and τt become the left and right sub-trees of node b.

# Example 10.6 Construct an AVL tree by inserting the following elements in the given order.

63, 9, 19, 27, 18, 108, 99, 81.

# Solution

![](bbox=[0.13, 0.31, 0.9, 0.73])

Figure 10.47 AVL tree

# Deleting a Node from an AVL Tree

Deletion of a node in an AVL tree is similar to that of binary search trees. But it goes one step ahead. Deletion may disturb the AVLness of the tree, so to rebalance the AVL tree, we need to perform rotations. There are two classes of rotations that can be performed on an AVL tree after deleting a given node. These rotations are r rotation and l rotation.

On deletion of node x from the AVL tree, if node a becomes the critical node (closest ancestor on the path from x to the root node that does not have its balance factor as 1, 0, or -1), then the type of rotation depends on whether x is in the left sub-tree of a or in its right sub-tree. If the