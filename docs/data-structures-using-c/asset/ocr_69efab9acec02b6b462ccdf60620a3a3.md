node of a binary tree. There are many operations that are often performed on a tree such as search a node, print some information, insert a node, delete a node, and so on. All such operations need the traversal through a tree.

This operation is used to visit each node (exactly once). A full traversal of a tree visits nodes of a tree in a certain linear order. This linear order could be familiar and useful. For example, if the binary tree contains an arithmetic expression, then its traversal may give us the expression in infix, postfix, or prefix notations.

There are various traversal methods. For a systematic traversal, it is better to visit each node (starting from the root) and its two subtrees in the same way. In other words, when traversing, we need to treat each node and its subtree in the same fashion. If we let L, D, and R stand for moving left, data, and moving right, respectively Fig. (7.32), when a node is left, then there are six possible combinations—LDR, LRD, DLR, DRL, RLD, and RLD.

![](bbox=[0.76, 0.24, 0.89, 0.31])

Fig. 7.32 Components of a subtree

Consider the binary tree shown in Fig. 7.33. This tree represents a binary tree. We have studied all the notations of an expression tree and its inter-conversions in Chapter 3.

![](bbox=[0.35, 0.46, 0.75, 0.6])

Fig. 7.33 A binary tree representing an arithmetic expression

Let us see the result of each of the six traversals.

| Traversal | Result |
| :--- | :--- |
| LDR: | 5-6+3x8/4 |
| LRD: | 56-384/x+ |
| DLR: | +-56x3/84 |
| DRL: | +x/483-65 |
| RDL: | 4/8x3-6-5 |
| RLD: | 48/3x65-+ |

We can notice that DLR and RLD, LDR and RDL, and LRD and DRL are mirror symmetric. If we adopt the convention that traversing is done left before right, only then, the three traversals, that is, LDR, LRD, and DLR, are fundamental. These are called as