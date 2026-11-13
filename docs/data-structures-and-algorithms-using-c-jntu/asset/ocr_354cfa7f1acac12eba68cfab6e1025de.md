# Operations

+   - isEmpty(ROOT)
+     Checks whether binary tree is empty.
+   - TRAVERSE_LCHILD(N)
+     Traversing the left subtree of node N by moving down its LCHILD pointer.
+   - TRAVERSE_RCHILD(N)
+     Traversing the right subtree of node N by moving down its RCHILD pointer.
+   - INSERT(ROOT,ITEM)
+     Insert a node with ITEM as DATA as the root node.
+   - LEFT_INSERT(N,ITEM)
+     Insert a node with ITEM as DATA as left child of a node N.
+   - RIGHT_INSERT(N,ITEM)
+     Insert a node with ITEM as DATA as right child of a node N.
+   - DELETE(ROOT)
+     Delete root node of a binary tree.
+   - DELETE_LCHILD(N)
+     Delete the left child of a node N.
+   - DELETE_RCHILD(N)
+     Delete the right child of a node N.
+   - ADD_DATA(LOC,ITEM)
+     Add ITEM into a node whose address is in LOC.
+   - RETRIEVE_DATA(LOC,ITEM)
+     Retrieve data of a node whose address is LOC.
+   - INORDER(T)
+     Perform inorder traversal on binary tree T.
+   - PREORDER(T)
+     Perform preorder traversal on binary tree T.
+   - POSTORDER(T)
+     Perform postorder traversal on binary tree T.

# SUMMARY

+   - A tree is a finite set of one or more nodes. Every node in a tree represents a unit of information. The links/arcs between the nodes are known as branches.
+   - A binary tree T is a finite set of elements. An empty tree is a binary tree.
+   - A binary tree of height h that consists of maximum permissible number of children to all nodes, i.e. 2^h -1 nodes is known as a full binary tree.
+   - A binary tree that has maximum permissible number of nodes at all the levels except the last level is known as a complete binary tree. A binary tree that has only left or right children is known as a skewed binary tree.
+   - Binary trees can be represented using both sequential and linked data structures.
+   - Various operations can be performed on binary trees such as searching, insertion, deletion, copy and display.