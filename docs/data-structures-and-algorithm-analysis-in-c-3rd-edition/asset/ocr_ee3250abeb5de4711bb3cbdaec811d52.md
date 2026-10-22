![](bbox=[0.07, 0.06, 0.92, 0.38])

# Figure 13.4 Example of an insert operation that violates the AVL tree balance property.

Prior to the insert operation, all nodes of the tree are balanced (i.e., the depths of the left and right subtrees for every node differ by at most one). After inserting the node with value 5, the nodes with values 7 and 24 are no longer balanced.

# 13.2.1 The AVL Tree

The AVL tree (named for its inventors Adelson-Velskii and Landis) should be viewed as a BST with the following additional property: For every node, the heights of its left and right subtrees differ by at most 1. As long as the tree maintains this property, if the tree contains n nodes, then it has a depth of at most O(log n). As a result, search for any node will cost O(log n), and if the updates can be done in time proportional to the depth of the node inserted or deleted, then updates will also cost O(log n), even in the worst case.

The key to making the AVL tree work is to alter the insert and delete routines so as to maintain the balance property. Of course, to be practical, we must be able to implement the revised update routines in Θ(log n) time.

Consider what happens when we insert a node with key value 5, as shown in Figure 13.4. The tree on the left meets the AVL tree balance requirements. After the insertion, two nodes no longer meet the requirements. Because the original tree met the balance requirement, nodes in the new tree can only be unbalanced by a difference of at most 2 in the subtrees. For the bottommost unbalanced node, call it S, there are 4 cases:

+   1. The extra node is in the left child of the left child of S.
+   2. The extra node is in the right child of the left child of S.
+   3. The extra node is in the left child of the right child of S.
+   4. The extra node is in the right child of the right child of S.

Cases 1 and 4 are symmetrical, as are cases 2 and 3. Note also that the unbalanced nodes must be on the path from the root to the newly inserted node.

Our problem now is how to balance the tree in O(log n) time. It turns out that we can do this using a series of local operations known as rotations. Cases 1 and