![](bbox=[0.12, 0.08, 0.88, 0.3])

# Figure 12.12 General representation of LR rotation

C and A are nodes with balance factors as +1 and 0, respectively. A_L and A_R are subtrees of A and C_R is the right subtree of C.

Inserting some node X as a right subtree of A, i.e. in X_R, changes the balance factor of A from 0 to -1 and C from +1 to +2. A new node is inserted as a right subtree (R) of left subtree (L) of the closest ancestor node C and this leads to an imbalance of tree. This is shown in Figure 12.12(b). In order to rebalance the tree LR rotation is invoked. This rotation pushes the new node X up to the place of C, the ancestor node where the imbalance is observed. C is shifted to the position of its right subtree C_R. Figure 12.12(c) shows the balanced AVL search tree after LR rotation in which X is the root and A is the left subtree with A_L as its left subtree and X_L the earlier left subtree of X as its right subtree. C is the right subtree with X_R the earlier right subtree of X as its left subtree and C_R as its right subtree.

+   Here, balance factors of nodes A and C after LR rotation are based on the balance factor of the new node after insertion and before rotation.
+   if bf(x)=0 then bf(A) and bf(C) will also be 0 after rotation
+   if bf(x)=1 then bf(A)=0 and bf(C)=-1 after rotation
+   if bf(x)=-1 then bf(A)=1 and bf(C)=0 after rotation.

![](bbox=[0.12, 0.65, 0.88, 0.82])

# Figure 12.13 Example of LR rotation