
Consider an instance of RR rotation depicted in Figure 12.17. The balanced AVL search tree before insertion is shown in Figure 12.17(a). After inserting node V as right subtree of right subtree, i.e. as the right subtree of T the balance factor of all the nodes in the path from root P to the newly inserted node V changes and makes the tree imbalanced as shown in Figure 12.17(b). The balance factor of T and S changed from 0 to -1 and that of P changed from -1 to -2. RR rotation is invoked to rebalance the tree. This pushes S up into the place of P and P now becomes the left subtree of S. Node Q earlier the left subtree of S now becomes the right subtree of P. The balanced AVL search tree after RR rotation is shown in Figure 12.17(c) with the balance factor of all the nodes as either 0 or -1.

## RL Rotation:

The general representation of RL rotation is depicted in Figure 12.16.

![](img/45784b9f0334626143002ec0d63692fd_401_0.png)

Figure 12.18 General representation of RL rotation

The balanced AVL search tree prior to insertion with nodes C and E having balance factors as -1 and 0, respectively, is shown in Figure 12.18(a). E_L and E_R are subtrees of E and C_L is the left subtree of C. Insertion of some element X has a left subtree (L) of a right subtree (R) leads to R, type imbalance of that tree by changing the balance factor of the closest ancestor node C from -1 to -2. The balance factor of E is also changed from 0 to +1. This is shown in Figure 12.18(b). The RL rotation is called to rebalance the tree. This rotation shifts the new node X up into the place of the ancestor node C and C is pushed into the place of its left subtree. Now X is with the left subtree C along with its left subtree C_L and X as its right subtree which was earlier the left subtree of X. Node E is now the right subtree of X with E_R as its right subtree and X_R as its left subtree which was earlier the right subtree of X. Now the tree is a balanced AVL search tree after RL rotation. This is shown in Figure 12.18(c).

Consider the instance of RL rotation shown in Figure 12.19. The balanced AVL search tree prior to the insertion is shown in Figure 12.19(a). After the new node Q is inserted as a left subtree of a right subtree, the balance factors in the path from root P to Q are changed. The balance factors of S and T changed from 0 to +1 and that of P changed from -1 to -2 which made the tree the RL type imbalance. This is shown in Figure 12.19(b). The RL rotation is invoked to rebalance the tree. This rotation shifts the parent of the new node S into the place of the ancestor node P and P is moved down into the place of its left subtree along with node M. The new node Q becomes the right subtree of P which was earlier the left subtree of S. Now tree is with balanced heights of subtrees with all the nodes having the balance factors as either 0 or +1. Hence, the tree is a balanced AVL search tree after RL rotation.

![](img/45784b9f0334626143002ec0d63692fd_402_0.png)

### (a) Balanced AVL search tree before insertion
### (b) Unbalanced AVL search tree after inserting Q
### (c) Balanced AVL search tree after RL rotation
## Figure 12.19 Example of RL rotation

The transformations that are performed to solve the LL and RR type imbalances are known as single rotations, and that of LR or RL type imbalances are known as double rotations. The transformation of LR type imbalance can be considered as the sequence of an RR rotation followed by an LL rotation, and that of RL type imbalance can be considered as an LL rotation followed by RR rotation.

## Algorithm 12.4 Insertion into an AVL tree

- 1. GETNODE (X)
- 2. DATA(X) = element
- 3. LCHILD(X) = RCHILD(X) = NULL and bf(X) = 0
- 4. If the tree T is empty then
  - (a) Set T to X.
  - (b) Exit.
  - //when AVL search tree T is non empty.
- 5. Starting from the root search the place to insert the new element.
- 6. Identify the most recently seen node with balance factor of either -1 or +1 as the ancestor node A.
- 7. If the element already exists
  - (i) Print "Insertion not possible as the element already exists".
  - (ii) Exit.
- 8. If no ancestor node A exists then update the balance factors in the path from root and exit.
- 9. If ancestor node A is found then
  - (a) If (bf(A) == +1 and the new node is inserted in the right subtree of A) or (bf(A) == -1 and the new node is inserted in the left subtree of A) then
    - (i) bf(A) = 0.
    - (ii) Update the balance factors of all the nodes on the path from A to the newly inserted node.
    - (iii) Exit.
  - (b) Else
    - (i) Recognize the type of imbalance at A and execute the appropriate rotation.
    - (ii) Update the balance factors of nodes in the path from new subtree root to the newly inserted node as needed by the rotation.
    - (iii) Reset the left and right subtrees of the corresponding nodes.
  - (c) Exit
- 10. End. The time complexity of insertion operation into an AVL search tree is O(height)=O(log n).

## 12.5.3 Deletion

Deletion of an element from an AVL search tree may also cause imbalance similar to insertion, rotations are invoked to rebalance the tree after deletion. Major classification of rotations are as L and R which can be further categorized as L0, L1, L-1 regarding L rotations and R0, R1, R-1 regarding R rotations.

Let p be the parent of the node that was deleted. Due to deletion the balance factors of some or all of the nodes on the path from the root to p might be changed. It is required to update the balance factors from node p to the root in the upward direction. All the deletions may not call the rotations. They are referred to as rotation-free deletions.

The following observations can be made regarding deletion:

- 1) If the node was deleted from the right subtree of p then bf(p) increases by 1 and if it was from the left subtree of p then bf(p) decreases by 1.
- 2) The height of the tree is decreased by 1 when the new bf(p) = 0. It is required to update the balance factor of its parent and/or its ancestors.
- 3) The height of the tree remains the same when the new bf(p) = +1 or -1 and there will be no change in the balance factors of its ancestor nodes.
- 4) The tree is imbalanced at node p when the new bf(p) = +2 or -2, and hence corresponding rotations are to be invoked.

In this process the balance factors of some nodes may become +2 or -2. In the path from p to the root the first node among them is A, the ancestor node. At node A the balance has to be restored, so the imbalance can be classified as type L when the deletion is from the left subtree of A and it is of type R when the deletion is from the right subtree of A.

Regarding type L, the bf(A) would have been -1 prior to deletion when it is now -2; bf(A) = -2. Ancestor node A might have a right subtree with root B. With respect to the bf(B) the L type rotations are further classified as L0 if bf(B)=0, L1 if bf(B)=+1 and L-1 if bf(B)=-1.

Regarding type R, the bf(A) would have been +1 prior to the deletion when it is now +2; bf(A)=+2. Ancestor node A might have a left subtree with root B. With respect to the bf(B) the R type rotations are further classified as R0 if bf(B)=0, R1 if bf(B)=+1 and R-1 if bf(B)=-1.

### R category rotations:

The following are the three types of R category rotations. They are explained along with representation and example.

### R0 rotation:

General representation of R0 rotation is illustrated in Figure 12.20. Some node X is to be deleted from right subtree of C, i.e. C_R. After deleting it, the balance factor of C changed from +1 to +2. Node B the left subtree of C has a balance factor of 0. So, R0 rotation is to be used to rebalance the tree. It pushes B into the place of C along with its left subtree B_L and C is shifted down into the place of its right subtree along with the C_R and B_L as its left subtree, the earlier right subtree of B. Here C_R is the right subtree of C after deletion.

![](img/45784b9f0334626143002ec0d63692fd_404_0.png)

(a) Balanced AVL search tree before deletion

(b) Unbalanced AVL search tree after deletion

(c) Balanced AVL search tree after deletion

## Figure 12.20 General representation of R0 rotation

![](img/45784b9f0334626143002ec0d63692fd_404_1.png)

(a) Balanced AVL search tree before deletion

(b) Unbalanced AVL search tree after deletion

![](img/45784b9f0334626143002ec0d63692fd_404_2.png)

(c) Balanced AVL search tree after R0 rotation

## Figure 12.21 Example of R0 rotation

Consider Figure 12.21 an instance of R0 rotation. From the balanced AVL search tree shown in Figure 12.21(a) the node R is deleted and bf(Q) is changed from 0 to 1. Also the bf(P) the ancestor node is also changed to +2 from +1 which calls R0 rotation as its left subtree, root M has the 0 balance factor. The unbalanced tree is shown in Figure 12.21(b). The balanced AVL search tree after R0 rotation and node M as the root is shown in Figure 12.21(c).
