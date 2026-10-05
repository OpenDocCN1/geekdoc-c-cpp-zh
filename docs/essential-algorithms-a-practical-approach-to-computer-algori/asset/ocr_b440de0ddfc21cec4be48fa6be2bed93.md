Similar techniques let you rebalance the tree in the right-left case. Use a right rotation to put the tree in the right-right case, and then use a left rotation to rebalance the tree.

# Deleting Values

You can use the same rotations to rebalance the tree whether you're adding new nodes or removing existing nodes. For example, Figure 11-5 shows the process of removing a node from an AVL tree. The top image shows the original tree. After node 1 is removed, the tree in the middle of the figure is unbalanced at node 3, because node's left subtree has height 1, and its right subtree has height 3. A left rotation gives the rebalanced tree shown on the bottom.

![](bbox=[0.188, 0.333, 0.477, 0.789])

**Figure 11-5**: A left rotation rebalances the tree after node 1 is removed.

At all times, an AVL tree containing N nodes has height at most O(log N), so it is reasonably short and wide. That means operations that climb the tree, such as searching for a value, take O(log N) time.