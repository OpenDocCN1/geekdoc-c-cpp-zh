# 14.3.1 SEARCHING

The process of searching for an element in a red-black tree is exactly the same as an element that is searched in a binary search tree. So, Algorithm 12.1 serves the purpose of search operation in a red-black tree.

# 14.3.2 INSERTION

Insertion of an element into a red-black tree is the same as that of into a binary search tree. To the new node either black or red colour must be set. Prior to the insertion if the tree was empty then black colour may be set to the new node as it becomes the root. If the tree is non-empty and the new node is set to black then it violates the third property of the definition as an additional black node appears in the path from a root node to an external node. If the new node is set to red colour it may violate the second property of the definition. This leads to the imbalance of the tree and needs to be rebalanced. So, it is obvious to set the new node with red colour because this may or may not violate the definition. But, if the new node is set to black then it definitely violates the definition.

When it is a case of imbalance, along with the new node x its parent node px must be red in colour, the two consecutive red nodes. Node px cannot be the root so, the grandparent of x, gx must exist and must be black in colour. The imbalance may be classified based on the position of the new node x with respect to its parent (px) and grandparent (gx), and colour of the other child of the grandparent (gx).

If the new node x is inserted as a left child of its parent px, which is again a left child of the grandparent of x, gx and colour of other child of the grandparent gx is black then it is an LLr type imbalance. If x is left child of px, px is a left child of gx and the other child of gx is red then it is an LRr type imbalance. If x is a right child of px, px is a left child of gx and the other child of gx is black then it is an LRb type imbalance. Similarly other imbalances are RLb, RLr, RRb and RRr.

The tree with imbalances, which have red as the colour of other children of the grandparent gx, LLR, LLR, LRr and RRr are rebalanced by changing colours of nodes. The other type imbalances, which have black as the colour of other children of the grandparent gx, LLb, RLb, LRb and RRb of the tree are rebalanced by rotation mechanism.

Llr, LRr, RRr and RLr imbalances: The general representation of LLR, LRr, RRR and RLr imbalances, the changes in node colour to rebalance the tree are illustrated in Figure 14.3. The classification of imbalance is depicted by L, R and r notations on the edges of the red-black trees.

![](bbox=[0.15, 0.69, 0.45, 0.88])

![](bbox=[0.55, 0.69, 0.85, 0.88])