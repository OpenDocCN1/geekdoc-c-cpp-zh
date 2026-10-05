# 176

# Chap. 5 Binary Trees

![](bbox=[0.368, 0.193, 0.623, 0.303])

**Figure 5.17** An example of removing the value 37 from the BST. The node containing this value has two children. We replace value 37 with the least value from the node's right subtree, in this case 40.

right subtree. We then substitute 40 as the new value for the root node. Figure 5.17 illustrates this process.

When duplicate node values do not appear in the tree, it makes no difference whether the replacement is the greatest value from the left subtree or the least value from the right subtree. If duplicates are stored, then we must select the replacement from the right subtree. To see why, the greatest value in the left subtree $G$. If multiple nodes in the left subtree have value $G$, selecting $G$ as the replacement for the root of the right subtree will result in a tree with equal values to the left of the node now containing $G$. Precisely this situation occurs if we replace value 120 with the greatest value in the left subtree of Figure 5.13(b). Selecting the value from the right subtree does not have a similar problem, because it does not violate the Binary Search Tree Property if equal values appear in the tree.

From the above, we see that if we want to remove the record stored in a node with two children, then we simply call `delete` on the node's right subtree and substitute the record for the record being removed. Figure 5.18 shows an implementation for `removehelp`.

The cost for **find** and **insert** is the depth of the node found or inserted. The cost for **removehelp** is the depth of the node being removed, or in the case when the node has two children, the depth of the node with smallest value in its right subtree. Thus, in the case, the cost for any one of these operations is the depth of the node. This is why it is desirable to keep BSTs **balanced**, that is, with least possible height. If a binary tree is completely unbalanced, for example in the shape of a linked list, then the height for a tree with $n$ nodes can be great as $n$. the nodes can be as great as $n$. Thus, a balanced BST in the average case have operations costing $\Theta(\log n)$, while a wildly unbalanced BST can have operations in the worst case $\Theta(n)$. Consider the situation where we construct a BST of $n$ nodes by inserting records one at a time. If we are fortunate to have them arrive in an order that results in a balanced tree (a “random” order is