152

Chap. 5 Binary Trees

![](bbox=[0.398, 0.185, 0.594, 0.335])

**Figure 5.1** A binary tree. Node $A$ is the root. Nodes $B$ and $C$ are $A$'s children. Nodes $B$ and $D$ form a subtree. Node $B$ has two children: its left child is the empty tree and its right child is $D$. Nodes $A, C,$ and $E$ are ancestors of $G$. Nodes $D, E,$ $	ext{and}$ $F$ make up level 2 of the tree; node $A$ is at level 0. The edges from $A$ to $C$ to $E$ to $G$ form a path of length 3. Nodes $D, G,$ and $I$ are leaves. Nodes $A, B, C,$ and $F$ are internal nodes. The depth of $I$ is 5. The height of this tree is 4.

root of the tree, while the root is the ancestor of all nodes. The **depth of a node $M$** in the tree is the length of the path from the root to $M$. The **height of a node** is one more than the depth of the deepest node in the tree. All nodes of depth $d$ are **leaf** in the tree. The only node at level 0, and its depth is 0. An **internal node** is any node that has at least one non-empty child.

Figure 5.1 illustrates the various used to identify properties of a binary tree. Figure 5.2 illustrates that binary trees have two children (one or both of which might be empty), the two trees of Figure 5.2 **are not the same**.

Two restricted forms of binary tree are sufficiently important to warrant special names. Each node in a **full** binary tree is either (1) an internal node with exactly two non-empty children or (2) a leaf. A **complete** binary tree has a restricted shape by starting at the root and filling the tree from left to right. All nodes except possibly level $d-1$ are completely filled. The bottom tree has its nodes filled from the left side.

Figure 5.3 illustrates the differences between full and complete binary trees.¹ There is no particular relationship between these two shapes; that, the tree of Figure 5.3(a) is full but not complete the tree of Figure 5.3(b) is complete but

> ¹While these definitions for full and complete binary tree are the most commonly used, they are not universal. Because the common meaning of the words "full" and "complete" are quite similar, there is little that you can do to distinguish between them other than to memorize the definitions. Here is a memory aid that you might find useful: "Complete" is a wider word than "full," and complete binary trees tend to be wider than full binary trees because each level of a complete binary tree is as wide as possible.