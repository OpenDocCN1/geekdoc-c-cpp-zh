
![](img/45784b9f0334626143002ec0d63692fd_396_0.png)

(a) Balanced AVL search tree before insertion

![](img/45784b9f0334626143002ec0d63692fd_396_1.png)

(b) Unbalanced AVL search tree after inserting B

![](img/45784b9f0334626143002ec0d63692fd_396_2.png)

(c) Rebalanced AVL search tree

Figure 12.9 Insertion into an AVL search tree

- 3. Insertion may affect the balance factors of only those nodes that appear on the path from the root to the new node that is inserted.
- 4. The nearest ancestor A of the newly inserted node whose balance factor is either +2 or -2 initiates the rotation.

In an AVL search tree, prior to the insertion, if the balance factor of all the nodes on the path from the root node to the currently inserted node was 0, then the tree will not become unbalanced even after insertion. Because the insertion will make the balance factor to change by -1, 0 or 1.

If the insertion makes an AVL search tree unbalanced, the height of the subtree must be adjusted by rotating them approximately with respect to the closest ancestor so that it is balanced.

Based on the place where the new node is inserted, that causes the imbalance rotations are classified into four types such as

- 1. LL rotation—new node inserted as the left subtree (L) of the left subtree (L) of A.
- 2. LR rotation—new node inserted as the right subtree (R) of the left subtree (L) of A.
- 3. RR rotation—new node inserted as the right subtree (R) of the right subtree (R) of A.
- 4. RL rotation—new node inserted as the left subtree (L) of the right subtree (R) of A.

LL rotation: General representation of LL rotation is illustrated in Figure 12.10. This figure shows how insertion leads to LL type imbalance and how the rotation is made to balance the tree again. Figure 12.10(a) shows the balanced AVL search tree before insertion in which B, C are with balance factors 0, +1, respectively. B_L, B_R and C_R are the subtrees of B and C.

(+1) C
(0) B   C_R
B_L  B_R

(a) Balanced AVL search tree before insertion

(+2) C
(+1) B   C_R
X
X_L  X_R

(b) Unbalanced AVL search tree after insertion of X into B_L

(0) B
(0) X   C (0)
X_L  X_R   B_R  C_R

(c) Balanced AVL search tree after LL rotation

Figure 12.10 General representation of LL rotation

In this a new node called X is inserted as a left subtree (L) of left subtree (L) of C, the ancestor node. Now the balance factors of B change from 0 to +1 and C changes from +1 to +2 and the tree is unbalanced; this is shown in Figure 12.10(b). To rebalance the tree LL rotation must be invoked. This rotation pushes B up into place of C and C is moved into the place of its right subtree earlier. The new node remains as the left subtree of B and B_R, earlier right subtree of B is now the left subtree of C along with its right subtree, C_R remained as it was. This is shown in Figure 12.10(c) where the height of the subtree is balanced and the balance factor of all nodes is 0. Hence, the AVL search tree is balanced after LL rotation.

(+1) P
(0) G   R (0)
(0) E   M (0)

(a) Balanced AVL search tree before insertion

(+2) P
(+1) G   R (0)
(+1) E   M (0)
(0) B

(b) Unbalanced AVL search tree after insertion of B

(0) G
(+1) E   P (+1)
(0) B   M (0)   M (0)   R (0)

(c) Balanced AVL search tree after LL rotation

Figure 12.11 Example for LL rotation

Consider Figure 12.11 which is an instance of LL rotation. Figure 12.11(a) shows an AVL search tree prior to insertion. Insertion of an element B as a left subtree of left subtree of ancestor node P, whose balance factor with insertion has changed from +1 to +2 disturbed the balance of the tree. This is shown in Figure 12.11(b). LL rotation shifts G up into the place of P and P is moved down along with its right subtree R. Node M, earlier right subtree of G, now becomes the left subtree of P. It can be observed from Figure 12.11(c) that the height of the tree is balanced and all the balance factors are either -1 or 0 or +1. General representation of LR rotation is depicted in Figure 12.12. It illustrates how an insertion leads to LR type imbalance and rebalancing the tree using corresponding rotation. Figure 12.12(a) shows a balanced AVL search tree prior to insertion. In this tree

![](img/45784b9f0334626143002ec0d63692fd_398_0.png)

Figure 12.12 General representation of LR rotation

C and A are nodes with balance factors as +1 and 0, respectively. A_L and A_R are subtrees of A and C_R is the right subtree of C.

Inserting some node X as a right subtree of A, i.e. in A_R, changes the balance factor of A from 0 to -1 and C from +1 to +2. A new node is inserted as a right subtree (R) of left subtree (L) of the closest ancestor node C and this leads to an imbalance of tree. This is shown in Figure 12.12(b). In order to rebalance the tree LR rotation is invoked. This rotation pushes the new node X up to the place of C, the ancestor node where the imbalance is observed. C is shifted to the position of its right subtree C_R. Figure 12.12(c) shows the balanced AVL search tree after LR rotation in which X is the root and A is the left subtree with A_L as its left subtree and X_L the earlier left subtree of X as its right subtree. C is the right subtree with X_R the earlier right subtree of X as its left subtree and C_R as its right subtree.

- Here, balance factors of nodes A and C after LR rotation are based on the balance factor of the new node after insertion and before rotation.
- if bf(x)=0 then bf(A) and bf(C) will also be 0 after rotation
- if bf(x)=1 then bf(A)=0 and bf(C)=-1 after rotation
- if bf(x)=-1 then bf(A)=1 and bf(C)=0 after rotation.

![](img/45784b9f0334626143002ec0d63692fd_398_1.png)

Figure 12.13 Example of LR rotation

Consider Figure 12.13, an instance of LR rotation. Figure 12.13(a) shows the balanced AVL search tree prior to insertion. After inserting F as a right subtree of left subtree of the closest ancestor G, the balance factor of the nodes in the path from the root to the newly inserted node is changed. Balance factor of node E has been changed from 0 to -1 and that of node G and node P has been changed from +1 to +2. The tree becomes imbalanced as shown in Figure 12.13(b). The LR rotation shifts F, the new node into the place of G and G is pushed down as the right subtree of E. Now, the tree is once again a balanced AVL search tree as shown in Figure 12.13(c) with the balance factors of all the nodes as +1 or 0.

![](img/45784b9f0334626143002ec0d63692fd_399_0.png)

(a) Balanced AVL search tree before insertion (b) Unbalanced AVL search tree after insertion into B_R (c) Balanced AVL search tree after LR rotation Figure 12.14 General representation of complex LR rotation

Figure 12.14 shows the general representation of complex LR rotation. Figure 12.14(a) shows balanced AVL search tree prior to insertion. Here C is with the balance factor +1, nodes A and B are with 0 balance factor. After inserting some node X as the right subtree (R) of left subtree (L) into B, then the balance factor of C changes to +2 from +1, nodes A and B change to -1 from 0. Now, the tree is unbalanced as shown in Figure 12.14(b). LR rotation is invoked to rebalance the tree. After rotation the tree is balanced as shown in Figure 12.14(c).

![](img/45784b9f0334626143002ec0d63692fd_399_1.png)

(a) Balanced AVL search tree before insertion (b) Unbalanced AVL search tree after inserting I (c) Balanced AVL search tree after LR rotation Figure 12.15 Example of LR rotation

Consider Figure 12.15, an instance of LR rotation. Figure 12.15(a) shows the balanced AVL search tree prior to insertion. After inserting I as the right subtree of the left subtree of the closest ancestor G, the balance factor of the nodes in the path from the root to the newly inserted node is changed. The balance factor of nodes G and H has been changed from 0 to -1 and node P has been changed from +1 to +2. This leads to the imbalance of the tree as shown in Figure 12.15(b). Invoke LR rotation, this shifts H up into the place of P and P is pushed down as its right subtree along with S. Now the node I becomes the left subtree of P. The rebalanced AVL search tree is shown in Figure 12.15(c).

![](img/45784b9f0334626143002ec0d63692fd_400_0.png)

(a) Balanced AVL search tree before insertion

(b) Unbalanced AVL search tree after insertion into D_R

(c) Balanced AVL search tree after RR rotation

Figure 12.16 General representation of RR rotation

RR rotation: The general representation of RR rotation is shown in Figure 12.16. The balanced AVL search tree prior to the insertion is shown in Figure 12.16(a). Here C and D are with the balance factors -1 and 0, respectively, D_L and D_R are the subtrees of D and C_L is the left subtree of C. When some element X is inserted as a right subtree (R) of the right subtree (R), i.e. in D_R. The balance factor of D changes from 0 to -1 and that of C, the closest ancestor changes from -1 to -2. This indicates that the tree got RR type imbalanced after insertion, and is shown in Figure 12.16(b). Invoking the RR rotation shifts node D up into the place of C and C is moved to be the left subtree of D. The new node X remained as the right subtree of D with X_L and X_R as its subtrees. Node C, along with its left subtree C_L as it was, has D_L earlier the left subtree of D, as its right subtree. Now the tree is a balanced AVL search tree after RR rotations with the balance factor as 0 for all the nodes. This is shown in Figure 12.16(c).

![](img/45784b9f0334626143002ec0d63692fd_400_1.png)

(a) Balanced AVL search tree before insertion

(b) Unbalanced AVL search tree after inserting V

(c) Balanced AVL search tree after RR rotation

Figure 12.17 Example of RR rotation
