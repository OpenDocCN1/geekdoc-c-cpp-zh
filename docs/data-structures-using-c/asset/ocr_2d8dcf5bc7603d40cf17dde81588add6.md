Here, 0 (zero) stored at Lchild or Rchild fields represents that the respective child is not present. Let us consider one more example as in Fig. 7.29.

In this node structure, Lchild and Rchild are the two link fields to store the addresses of left child and right child of a node; data is the information content of the node. With this representation, if we know the address of the root node, then using it, any other node can be accessed.

Each node of a binary tree (as the root of some subtree) has both left and right subtrees, which can be accessed through pointers as follows.

![](bbox=[0.32, 0.28, 0.76, 0.67])

![](bbox=[0.29, 0.7, 0.81, 0.9])