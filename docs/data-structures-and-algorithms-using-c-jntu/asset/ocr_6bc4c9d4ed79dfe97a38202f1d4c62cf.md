+   5. Call RETURN (NODE) .
+   CASE 3: When NODE has only left subtree
+   LCHILD of NODE=NULL and
+   RCHILD of NODE=NULL
+   1. Set TEMP to LCHILD of NODE
+   2. Set RCHILD of parent of NODE or LCHILD of parent of NODE to TEMP based
+   on whether NODE is right child or left child of its parent respectively.
+   3. Call RETURN (NODE).
+   CASE 4: When NODE has only right subtree
+   LCHILD of NODE=NULL and RCHILD of NODE= NULL
+   1. Set TEMP to RCHILD of NODE
+   2. Set RCHILD of parent of NODE or LCHILD of parent of NODE to TEMP based
+   on whether NODE is right child or left child of its parent respectively.
+   3. Call RETURN (NODE).
+   4. End case
+   5. End

# 12.3.4 Disadvantages of Binary Search Tree

A BST is highly efficient in performing all the operations with a time complexity of O(logn) over a sequential list. But, in the worst case where height h of the binary search tree is equal to the number of nodes n, its performance deteriorates. This happens because of its sequence of insertion and/or deletion operations which results in skewed BSTs with the time complexity of O(n). The binary search trees in Figure 12.7 show the skewed BSTs.

![](bbox=[0.08, 0.5, 0.9, 0.93])