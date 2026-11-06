The program should prompt the user for a value to locate in the list.

+   17. 19.22 (**Binary Tree Search**) Write member function `binaryTreeSearch`, which attempts to locate a specified value in a binary search tree object. The function should take as arguments a pointer to the binary tree’s root node and a search key to locate. If the node containing the search key is found, the function should return a pointer to that node; otherwise, the function should return a `nullptr` pointer.

+   18. 19.23 (**Level-Order Binary Tree Traversal**) The program of **Figs. 19.20–19.22** illustrated three recursive methods of traversing a binary tree—inorder, preorder and postorder traversals. This exercise presents the *level-order traversal* of a binary tree, in which the node values are printed level by level, starting at the root node level. The nodes on each level are printed from left to right. The level-order traversal is not a recursive algorithm. It uses a queue object to control the output of the nodes. The algorithm is as follows:
+   
+   A. Insert the root node in the queue
+   
+   B. While there are nodes left in the queue,
+      - Get the next node in the queue
+      - Print the node’s value
+      - If the pointer to the left child of the node is not `nullptr`
+        - Insert the left child node in the queue
+      - If the pointer to the right child of the node is not `nullptr`
+        - Insert the right child node in the queue.