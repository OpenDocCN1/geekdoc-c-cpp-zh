deleting an old entry, then it is much slower to use a contiguous sequential list than a linked list, as insert() and delete() operations need data movement. On the other hand, in a linked organization, we need only a few pointer manipulations for insertion and deletions. If so, we can then find an implementation for an ordered list where we can search quickly (as with binary search) and insert or delete elements quickly (as with linked list). A binary tree provides an excellent solution to this problem.

+   1. We can make entries of an ordered list into the nodes of a binary tree. We shall see that we can search a target key in O(log n) steps, and in addition, we can insert and delete the key in time O(log2 n).
+   2. The binary search tree (BST) is a binary tree with the property that the value in a node is greater than any value in a node's left subtree and less than any value in the node's right subtree.
+   3. This property guarantees fast search time provided the tree is relatively balanced.

The BSTs are classified as static trees and dynamic trees. Static tree is a BST where the set of values in the nodes is known in advance and never changes. Dynamic tree is a BST where the values in a tree may change over time. We shall study the ways of building and balancing these search trees to guarantee that the trees remain balanced so that the search time is minimum.

# **Binary search tree** A BST is a binary tree that is either empty or where every node contains a key and satisfies the following conditions:

+   1. The key in the left child of a node, if it exists, is less than the key in its parent node.
+   2. The key in the right child of a node, if it exists, is greater than the key in its parent node.
+   3. The left and right subtrees of a node are again BSTs.

The definition ensures that no two entries in a BST can have equal keys. It is possible to change the definition to allow entries with equal keys but doing so makes an algorithm more complicated. We assume that all keys are unique.

Figure 7.54 represents two BSTs.

![](bbox=[0.223, 0.683, 0.875, 0.833])

Fig. 7.54 Binary search trees