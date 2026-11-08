**Definition:** The level of a node in a binary tree is the number of branches on the path from the root to the node.

Clearly, the level of the root node of a binary tree is 0, and the level of the children of the root node is 1.

**Definition:** The height of a binary tree is the number of nodes on the longest path from the root to a leaf.

# EXAMPLE 19.2

Consider the binary tree of Figure 19-5. In this example, the terms such as node A and (node with info A) mean the same thing.

![](bbox=[0.35, 0.365, 0.78, 0.712])

**FIGURE 19-5**  Binary tree

In this binary tree, the nodes I, E, and H have no left and right children. So, the nodes I, E, and H are leaves.

There is a branch from node A to node B. So, node A is the parent of node B. Similarly, node A is the parent of node C, node B is the parent of nodes D and E, node C is the parent of node F, node D is the parent of node G, and so on.

A→B→D→G is a path from node A to node G. Because there are three branches on this path, the length of this path is 3. Similarly, B→D→G→I is a path from node B to node I.

There are three leaves in this binary tree, which are I, E, and H. Also, the paths from root to these leaves are: A→B→D→G→I, A→B→E, and A→C→F→H. Clearly, the longest path from