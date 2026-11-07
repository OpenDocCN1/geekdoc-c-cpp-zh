+   1. Traverse the left subtree of A; that is, traverse \(L_A = \{B, D\}\).
+   2. Visit A.
+   3. Traverse the right subtree of A; that is, traverse \(R_A = \{C\}\).

Now we cannot do Step 2 until we have finished Step 1.

+   1. Traverse the left subtree of A; that is, traverse \(L_A = \{B, D\}\). Now \(L_A\) is a binary tree with the root node B. Because \(L_A\) is a binary tree, we apply the inorder traversal criteria to \(L_A\).
+      1.1. Traverse the left subtree of B; that is, traverse \(L_B = \text{empty}\).
+      1.2. Visit B.
+      1.3. Traverse the right subtree of B; that is, traverse \(R_B = \{D\}\).

As before, first we complete Step 1.1 before going to Step 1.2.

+   1.1. Because the left subtree of B is empty, there is nothing to traverse. Step 1.1 is completed, so we proceed to Step 1.2.
+   1.2. Visit B. That is, output B on an output device. Clearly, the first node printed is B. This completes Step 1.2, so we proceed to Step 1.3.
+   1.3. Traverse the right subtree of B; that is, traverse \(R_B = \{D\}\). Now \(R_B\) is a binary tree with the root node D. Because \(R_B\) is a binary tree, we apply the inorder traversal criteria to \(R_B\).
+      1.3.1. Traverse the left subtree of D; that is, traverse \(L_D = \text{empty}\).
+      1.3.2. Visit D.
+      1.3.3. Traverse the right subtree of D; that is, traverse \(R_D = \text{empty}\).
+         1.3.1. Because the left subtree of D is empty, there is nothing to traverse. Step 1.3.1 is completed, so we proceed to Step 1.3.2.
+         1.3.2. Visit D. That is, output D on an output device. This completes Step 1.3.2, so we proceed to Step 1.3.3.
+         1.3.3. Because the right subtree of D is empty, there is nothing to traverse. Step 1.3.3 is completed.

This completes Step 1.3. Because Steps 1.1, 1.2, and 1.3 are completed, Step 1 is completed, so we go to Step 2.

+   2. Visit A; that is, output A on an output device. This completes Step 2, so we proceed to Step 3.

+   3. Traverse the right subtree of A; that is, traverse \(R_A = \{C\}\). Now \(R_A\) is a binary tree with the root node C. Because \(R_A\) is a binary tree, we apply the inorder traversal criteria to \(R_A\).
+      3.1. Traverse the left subtree of C; that is, traverse \(L_C = \text{empty}\).
+      3.2. Visit C.
+      3.3. Traverse the right subtree of C; that is, traverse \(R_C = \text{empty}\).