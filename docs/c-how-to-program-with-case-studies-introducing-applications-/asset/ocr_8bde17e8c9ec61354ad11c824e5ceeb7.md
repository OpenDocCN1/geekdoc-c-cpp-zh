>data the integer to store. Lines 57–58 assign `NULL` to `(*treePtr)->leftPtr` and `(*treePtr)->rightPtr`. Then control returns to the caller—either `main` or a previous call to `insertNode`.

+   2. If `*treePtr` is not `NULL` and the value to insert is less than `(*treePtr)->data`, line 66 recursively calls `insertNode` with the address of `(*treePtr)->leftPtr` to insert the new node in the left subtree of the node pointed to by `treePtr`.
+   3. If the value to insert is greater than `(*treePtr)->data`, line 69 recursively calls `insertNode` with the address of `(*treePtr)->rightPtr` to insert the node in the right subtree of the node pointed to by `treePtr`.

The recursive steps continue until `insertNode` finds a `NULL` pointer, then *Step 1* inserts the new node as a leaf node.

# 12.7.2 Traversals: Functions inOrder, preOrder and postOrder

Functions `inOrder` (lines 78–85), `preOrder` (lines 88–95) and `postOrder` (lines 98–105) each receive a pointer to a tree’s root node and traverse the tree. Below we describe the traversals and show the result of applying each for the following tree:

![](bbox=[0.365, 0.437, 0.635, 0.513])

# inOrder Traversal

The steps for an `inOrder` traversal are:

+   1. Traverse the *left* subtree `inOrder` (line 81).
+   2. Process the value in the node (line 82).
+   3. Traverse the *right* subtree `inOrder` (line 83).

This traversal processes each node’s value after processing the values in the left subtree. The inOrder traversal of the preceding tree is:

`6 13 17 27 33 42 48`

A binary search tree’s inOrder traversal processes the nodes in ascending order. Creating a binary search tree actually sorts the data. So, this process is called a binary tree sort.

# preOrder Traversal

The steps for a `preOrder` traversal are:

+   1. Process the value in the node (line 91).
+   2. Traverse the *left* subtree `preOrder` (line 92).
+   3. Traverse the *right* subtree `preOrder` (line 93).