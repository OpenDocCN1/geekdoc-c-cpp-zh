# FIGURE 10.2 More Examples of Binary Trees

# (a) A full binary tree

![](bbox=[0.38, 0.21, 0.62, 0.31])

# (b) A binary tree that is complete but not full

![](bbox=[0.16, 0.35, 0.46, 0.49])

# (c) A binary tree that is neither complete nor full

![](bbox=[0.58, 0.35, 0.85, 0.49])

**Ancestor.** A node's parent is its first **ancestor**. The parent of the parent is the next ancestor. The parent of the parent of the parent is the next ancestor ... and so on forth, until you reach the root. The root is an ancestor of each other node.

**Descendent.** A node's children are its first **descendants**. The children's children are its next descendants. The children of the children's children are ... well, you get the idea.

**Subtree.** Any node in a tree also can be viewed as the root of a new, smaller tree. This smaller tree contains the node that we've picked as the new root and all of the new root's descendants. This is called a **subtree** of the original tree. In Figure 10.2(a), we may choose 17 as the root of a new subtree, and that subtree has three nodes: the nodes containing 17, 9, and 53.

**Left and right subtrees of a node.** For a node in a binary tree, the nodes beginning with its left child and below are its **left subtree**. The nodes beginning with its right child and below are its **right subtree**.

**Depth of a node.** Suppose you start at a node _n_ and move upward to its parent. We'll call this "one step." Then move up to the parent of the parent—that's a second step. Eventually, you will reach the root, and the number of steps taken is called the **depth of the node** _n_. The depth of the root itself is zero; a child of the root has depth one. In Figure 10.2(b), the node containing 13 has depth three.