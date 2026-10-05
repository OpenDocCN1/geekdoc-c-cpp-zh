The final case occurs when the target node has two children and its left child has a right child. In that case, you should search the tree to find the rightmost node below the target node's left child. If that node has no children, simply replace the target node with it. If that node has a left child, replace it with its left child, and then replace the target node with the rightmost node.

Figure 10-11 shows this case where you want to remove node 35. 35 has two children, and its left child (17) has a right child (24). The algorithm moves down from the left child (17) as far as possible by following right child links. In this example, that leads to node 24, but in general that rightmost child could be further down the tree.

![](bbox=[0.137, 0.311, 0.633, 0.558])

**Figure 10-11:** Removing a target node with two children whose left child has a right child is the most complicated operation for a sorted binary tree.

To delete the target node, the algorithm replaces the rightmost node with its child (if it has one) and then replaces the target node with the rightmost node. In this example, the program replaces node 24 with node 23 and then replaces node 35 with node 24, resulting in the tree on the right in Figure 10-11.

# # Threaded Trees

A *thread* is a series of links that allow you to move through the nodes in a tree or network in any other way than following normal branches or links. A *threaded tree* is a tree that contains one or more threads.

For example, Figure 10-12 shows a tree with threads represented by dashed arrows.

The threads shown in Figure 10-12 point from a node to the nodes that come before and after it in an inorder traversal. They allow an algorithm to perform