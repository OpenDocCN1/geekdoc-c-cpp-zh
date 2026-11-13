The inorder traversal of a binary search tree produces the sorted list of the given elements in ascending order. The inorder traversal of the binary search trees shown in Figure 12.1(a) produces the sorted list as (22, 30, 40, 60, 70, 75), the ascending order of the given list (46, 60, 75, 30, 70, 22), and Figure 12.1(b) produces the sorted list as {8, M, N, P, T, Z}, the ascending order of the given list {M, P, 8, N, Z, T}).

# 12.2 REPRESENTATION OF A BINARY SEARCH TREE

Similar to the representation of a binary tree, a binary search tree is also represented in a linked representation manner. To illustrate the representation, consider the binary search tree depicted in Figure 12.1(a); its node structure and linked representation are given in Figure 12.2.

| LCHILD | DATA | RCHILD |

(a) Node structure of a binary search tree

![](bbox=[0.1, 0.35, 0.9, 0.58])

(b) Linked representation of a binary search tree of Figure 12.1(a)

Figure 12.2 Linked representation of a binary search tree

The null pointers of the nodes are not represented physically but are only fictitious and are known as external nodes. The external nodes depicted with solid circles are specified as e1. The path from the root to an external node is known as an external path. Thus, the linked representation of a binary search tree is a collection of internal nodes that represent the keys and external nodes that represent null pointers. This kind of binary tree is known as an extended binary tree.

# 12.3 OPERATIONS ON BINARY SEARCH TREES

Various operations can be performed on binary search trees but the most frequently used are search, insert and delete operations.

# 12.3.1 SEARCHING

In a binary search tree T searching for a key u is initiated at the root. If the key u is less than the key at the root then consider only the left subtree of T to search the key u. If the key u is greater than the key at the root then