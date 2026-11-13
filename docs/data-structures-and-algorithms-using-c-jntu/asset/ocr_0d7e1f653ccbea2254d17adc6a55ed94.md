Consider Figure 12.13, an instance of LR rotation. Figure 12.13(a) shows the balanced AVL search tree prior to insertion. After inserting F as a right subtree of left subtree of the closest ancestor G, the balance factor of the nodes in the path from the root to the newly inserted node is changed. Balance factor of node E has been changed from 0 to -1 and that of node G and node P has been changed from +1 to +2. The tree becomes imbalanced as shown in Figure 12.13(b). The LR rotation shifts F, the new node into the place of G and G is pushed down as the right subtree of E. Now, the tree is once again a balanced AVL search tree as shown in Figure 12.13(c) with the balance factors of all the nodes as +1 or 0.

![](bbox=[0.1, 0.23, 0.9, 0.43])

(a) Balanced AVL search tree before insertion (b) Unbalanced AVL search tree after insertion into B_R (c) Balanced AVL search tree after LR rotation Figure 12.14 General representation of complex LR rotation

Figure 12.14 shows the general representation of complex LR rotation. Figure 12.14(a) shows balanced AVL search tree prior to insertion. Here C is with the balance factor +1, nodes A and B are with 0 balance factor. After inserting some node X as the right subtree (R) of left subtree (L) into B, then the balance factor of C changes to +2 from +1, nodes A and B change to -1 from 0. Now, the tree is unbalanced as shown in Figure 12.14(b). LR rotation is invoked to rebalance the tree. After rotation the tree is balanced as shown in Figure 12.14(c).

![](bbox=[0.1, 0.64, 0.9, 0.84])

(a) Balanced AVL search tree before insertion (b) Unbalanced AVL search tree after inserting I (c) Balanced AVL search tree after LR rotation Figure 12.15 Example of LR rotation