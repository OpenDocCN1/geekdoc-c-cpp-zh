trees. If n = 3 then there are five distinct binary trees.

Consider the nodes of a binary tree of n nodes are numbered from 1 to n. The inorder permutation defined by such a binary tree is the order in which its nodes are visited during an inorder traversal of the tree. A preorder permutation can be defined similarly.

Now, if the nodes of a binary tree are numbered such that its preorder permutation is 1, 2...n then distinct binary tree define distinct inorder permutation. For example, if the nodes of binary tree numbers 1, 2, 3 then possible permutations obtain by a stack are

+   1, 2, 3
+   1, 3, 2
+   2, 1, 3
+   2, 3, 1
+   3, 2, 1

It is not possible to obtain 3, 1, 2. Each of these five permutations corresponding to one of the five distinct binary trees with three nodes.

![](bbox=[0.15, 0.3, 0.85, 0.39])

Figure 8.49: Five distinct binary trees with three nodes

It can calculate the total numbers of binary trees of n nodes by using Catalan numbers from a sequence of natural numbers.

C_n = \sum_{i=1}^n C_{i-1} C_{n-i} = \frac{1}{n+1} \binom{2n}{n} = \frac{(2n)!}{(n+1)!n!} \text{ for } n \ge 0

The Catalan numbers for n = 0, 1, 2, 3, 4, 5, 6... are 1, 1, 2, 5, 14, 42, 132...

# Multi-way Search Tree or M-way Search Tree

Although it is possible to use binary trees for fast searching, insertion and deletion in the internal memory (i.e. main memory), but binary trees are not appropriate for data that stored in external memory (i.e. storage devices such as disks etc.). When accessing data on a disk, an entire block (or page) of data is input at once. Therefore, it makes sure to design such tree special so that each node of the tree essentially occupies one entire block. Multi-way search tree, B-tree, B+ tree are examples of such data structures.

An m-way search tree (also known as multi-way search tree) of order m is a tree, which is either empty or for a non-empty m-way search tree has following properties:

+   i) All the nodes are of maximum m degree and any node contains maximum m-1 values.
+   ii) The nodes contain 1 to m-1 distinct keys K1, K2...Km-1 and keys in each node are sorted such that K1 < K2 < ... < Km-1.
+   iii) A node with n values has n+1 subtrees such that A0, A1, A2,...An. The subtrees may be empty.
+   iv) All the key values in the subtree Ai of a node [K1, K2,...Kn] may hold only values K in the range Ki <= K <= Ki+1.
+   v) All key values in the leftmost subtree A0 are less than K1.
+   vi) All key values in the rightmost subtree An are greater than Kn.
+   vii) All the subtrees are also m-way search trees.

However, m-way search trees can become unbalance.