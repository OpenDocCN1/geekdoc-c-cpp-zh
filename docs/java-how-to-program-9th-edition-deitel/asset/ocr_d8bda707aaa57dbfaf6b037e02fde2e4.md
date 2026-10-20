+   b) Set the reference in the parent of the node being deleted to reference the replacement node.
+   c) Set the reference in the parent of the replacement node to null.
+   d) Set the reference to the right subtree in the replacement node to reference the right subtree of the node to be deleted.
+   e) Set the reference to the left subtree in the replacement node to reference the left subtree of the node to be deleted.

The deletion steps for a replacement node with a left child are similar to those for a replacement node with no children, but the algorithm also must move the child into the replacement node’s position in the tree. If the replacement node is a node with a left child, the steps to perform the deletion are as follows:

+   a) Store the reference to the node to be deleted in a temporary reference variable.
+   b) Set the reference in the parent of the node being deleted to refer to the replacement node.
+   c) Set the reference in the parent of the replacement node to reference the left child of the replacement node.
+   d) Set the reference to the right subtree in the replacement node to reference the right subtree of the node to be deleted.
+   e) Set the reference to the left subtree in the replacement node to reference the left subtree of the node to be deleted.

Write method deleteNode, which takes as its argument the value to delete. Method deleteNode should locate in the tree the node containing the value to delete and use the algorithms discussed here to delete the node. If the value is not found in the tree, the method should display a message saying so. Modify the program of Figs. 22.17 and 22.18 to use this method. After deleting an item, call the methods inorderTraversal, preorderTraversal and postorderTraversal to confirm that the delete operation was performed correctly.

22.23 (Binary Tree Search) Modify class Tree of Fig. 22.17 to include method contains, which attempts to locate a specified value in a binary-search-tree object. The method should take as an argument a search key to locate. If the node containing the search key is found, the method should return a reference to that node’s data; otherwise, it should return null.

22.24 (Level-Order Binary Tree Traversal) The program of Figs. 22.17 and 22.18 illustrated three recursive methods of traversing a binary tree—inorder, preorder and postorder traversals. This exercise presents the level-order traversal of a binary tree, in which the node values are printed level by level, starting at the root node level. The nodes on each level are printed from left to right. The level-order traversal is not a recursive algorithm. It uses a queue object to control the output of the nodes. The algorithm is as follows:

+   a) Insert the root node in the queue.
+   b) While there are nodes left in the queue, do the following:
+      Get the next node in the queue.
+      Print the node’s value.
+      If the reference to the left child of the node is not null:
+        Insert the left child node in the queue.
+      If the reference to the right child of the node is not null:
+        Insert the right child node in the queue.

Write method levelOrder to perform a level-order traversal of a binary tree object. Modify the program of Figs. 22.17 and 22.18 to use this method. [Note: You’ll also need to use the queue-processing methods of Fig. 22.13 in this program.]

22.25 (Printing Trees) Modify class Tree of Fig. 22.17 to include a recursive outputTree method to display a binary tree object. The method should output the tree row by row, with the top of the tree at the left of the screen and the bottom of the tree toward the right. Each row is output vertically. For example, the binary tree illustrated in Fig. 22.20 is output as shown in Fig. 22.21.