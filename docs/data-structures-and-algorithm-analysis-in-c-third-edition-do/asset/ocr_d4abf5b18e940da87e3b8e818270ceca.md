# 5.8 Exercises

**5.4** Explain why function preorder from Section 5.2 makes half as many recursive calls as function preorder. Explain why it makes twice as many accesses to left and right children.

+   **5.5** (a) Modify the preorder traversal of Section 5.2 to perform an inorder traversal of a binary tree.

+   (b) Modify the preorder traversal of Section 5.2 to perform a postorder traversal of a binary tree.

**5.6** Write a recursive function search that takes input the pointer to the root of a binary tree (not a BST) and a value $K$, and returns true if value $K$ appears in the tree and false otherwise.

**5.7** Write an algorithm that takes input the pointer to the root of a binary tree and prints the values of the tree in level order. Level order first prints the root, then all nodes of level 1, then all nodes of level 2, and on. Hint: Preorder traversals make use of stack for recursive calls. Consider using another data structure to help implement the level-order traversal of a binary tree.

**5.8** Write a recursive function that returns the height of a binary tree.

**5.9** Write a recursive function that returns a count of the number of leaf nodes in a binary tree.

**5.10** Assume that a BST stores integer values in its nodes. Write a recursive function that sums the values of all nodes in the tree.

**5.11** Assume that a given BST stores integer values in its nodes. Write a recursive function that traverses a binary tree, and prints the value of every node who's grandparent has a value that is a multiple of five.

**5.12** Write a recursive function that traverses a binary tree, and prints the value of every node which has at least four great-grandchildren.

**5.13** Compute the overhead fraction for each of the following full binary tree implementations.

+   (a) All nodes data, two child pointers, and a parent pointer. The data field requires four bytes and each pointer requires four bytes.

+   (b) All nodes store data and two child pointers. The data field requires sixteen bytes and each pointer requires four bytes.

+   (c) All nodes store data and a parent pointer, and internal nodes store two child pointers. The data field requires eight bytes and each pointer requires four bytes.

+   (d) Only leaf nodes store data; internal nodes store two child pointers. The data field requires eight bytes and each pointer requires four bytes.

**5.14** Why is the BST Property defined so that nodes with values equal to the value of the root appear only in the right subtree, rather than allow equal-valued nodes to appear in either subtree?