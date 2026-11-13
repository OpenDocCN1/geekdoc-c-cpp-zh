# 8.10 Height Balanced Tree (AVL Tree)

A height balanced tree is a binary tree in which the difference in heights between the left and the right subtree is not more than one for every node.

The height of a tree is the number of nodes in the longest path from the root to any leaf.

The property of this tree is described by two Russian Mathematicians G.M. Adelson – vel'skii and E.M. Landis. There fore this tree is so called for their honour.

A Binary Search Tree in which the difference of heights of the right and left sub trees of any node is less than or equal to one is known as AVL tree.

While insertion of any node to the tree we have to find out the Balancing Factor which is the difference between the left height–right height.

+   The Balancing Factor is 1 than the tree is Left heavy
+   If the Balancing Factor is -1 than the tree is Right Heavy
+   If the Balancing Factor is 0 than the tree is Balanced

# INSERTION WITH AN AVL TREE

We can insert a new node into an AVL tree by first using the usual binary tree insertion technique, comparing the key of the new node with that in the root and inserting the new node into the left or right subtrees accurately.

But AVL tree has a property that the height of left and right subtree will be with maximum difference 1. Suppose after inserting new node, this difference becomes more than 1, i.e/ the value of the balance factor has some value other than -1,0,1. So now our work is to restore the property of AVL tree again.

To convert an unbalanced tree to AVL tree some rotations are needed such as

+   LR rotation
+   RL Rotation
+   LL rotation
+   RR notation