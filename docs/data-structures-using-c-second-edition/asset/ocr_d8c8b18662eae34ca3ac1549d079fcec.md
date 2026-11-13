node to be deleted is present in the left sub-tree of A, then L rotation is applied, else if x is in the right sub-tree, R rotation is performed.

Further, there are three categories of L and R rotations. The variations of L rotation are L-1, L0, and L1 rotation. Correspondingly for R rotation, there are R0, R-1, and R1 rotations. In this section, we will discuss only R rotation. L rotations are the mirror images of R rotations.

# R0 Rotation

Let b be the root of the left or right sub-tree of A (critical node). R0 rotation is applied if the balance factor of b is 0. This is illustrated in Fig. 10.48.

![](bbox=[0.18, 0.27, 0.82, 0.42])

Figure 10.48 R0 rotation in an AVL tree

Tree (a) is an AVL tree. In tree (b), the node x is to be deleted from the right sub-tree of the critical node A (node A is the critical node because it is the closest ancestor whose balance factor is not -1, 0, or 1). Since the balance factor of node b is 0, we apply R0 rotation as shown in tree (c).

During the process of rotation, node b becomes the root, with T1 and A as its left and right child. T2 and T3 become the left and right sub-trees of A.

# R1 Rotation

Let b be the root of the left or right sub-tree of A (critical node). R1 rotation is applied if the balance factor of b is 1. Observe that R0 and R1 rotations are similar to LL rotations; the only difference is that R0 and R1 rotations yield different balance factors. This is illustrated in Fig. 10.50.

# Example 10.7 Consider the AVL tree given in Fig. 10.49 and delete 72 from it.

# Solution

![](bbox=[0.11, 0.72, 0.5, 0.88])

Figure 10.49 AVL tree

Tree (a) is an AVL tree. In tree (b), the node x to be deleted from the right sub-tree of the critical node A (node A is the critical node because it is the closest ancestor whose balance factor is not -1, 0, or 1). Since the balance factor of node b is 1, we apply R1 rotation as shown in tree (c).

During the process of rotation, node b becomes the root, with T1 and A as its left and right children. T2 and T3 become the left and right sub-trees of A.