+   4. The ADT binary search tree has several methods that are the same as those in the ADT binary tree. However, its insertion, removal, and retrieval operations have different definitions than those for the ADT binary tree.
+   5. Operations on a binary search tree can be quite efficient. In the worst case, however—when the tree approaches a linear shape—the performance of its operations degrades and is comparable to that of a linear linked chain. If you must avoid such a situation for a given application, you should use the balancing methods presented in Chapter 19.
+   6. The tree sort algorithm efficiently sorts an array by using the binary search tree's insertion and traversal operations.
+   7. If you save a binary search tree's data in a file while performing an inorder traversal of its nodes, you can restore the tree as a binary search tree of minimum height. If you save a binary search tree's data in a file while performing a preorder traversal of its nodes, you can restore the tree to its original form.
+   8. You can use a binary tree to represent a general tree or an n-ary tree. However, an n-ary tree can have nodes that point to all of its children.

# EXERCISES

+   1. Consider the binary search tree in Figure 15-20 of Chapter 15. The numbers simply label the nodes so that you can reference them; they do not indicate the contents of the nodes.
+      a. Which node must contain the inorder successor of the value in the root? Explain.
+      b. Which node must contain the inorder predecessor of the value in the root? Explain.
+   2. Arrange nodes that contain the letters A, C, E, F, L, V, and Z into two binary search trees: one that has maximum height and one that has minimum height.
+   3. Consider the binary search tree in Figure 15-18 of Chapter 15.
+      a. What tree results after you insert the entries 80, 65, 75, 45, 35, and 25, in that order?
+      b. After inserting the nodes mentioned in part a, what results when you remove the entries 50 and 20?
+   4. Consider the binary search tree in Figure 15-19 of Chapter 15. What does the tree look like after you remove M, D, G, and T, in that order?
+   5. If you remove an item from a binary search tree and then insert it back into the tree, will you ever change the shape of the tree?
+   6. Suppose that the ADT binary tree has the operation
+      replace(item: ItemType, replacementItem: ItemType): boolean
+      It locates, if possible, the node in a binary tree that contains item and replaces item with replacementItem.
+      a. Add the operation replace to the link-based implementation of the ADT binary tree given in this chapter. The operation should replace an item without altering the tree structure.
+      b. Add the operation replace to the link-based implementation of the ADT binary search tree. Be sure that the tree remains a binary search tree.
+      c. Implement a method replace within a client of BinarySearchTree.