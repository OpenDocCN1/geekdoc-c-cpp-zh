the traversal operations—then you just saw for a binary tree apply to a binary search tree without change, because a binary search tree is a binary tree.

The operations that define the ADT binary search tree are as follows:

+   **Note: ADT binary search tree operations**
+   * Test whether a binary search tree is empty.
+   * Get the height of a binary search tree.
+   * Get the number of nodes in a binary search tree.
+   * Get the data in a binary search tree's root.
+   * Insert a new item into a binary search tree.
+   * Remove the given item from a binary search tree.
+   * Remove all entries from a binary search tree.
+   * Retrieve the given item from a binary search tree.
+   * Test whether a binary search tree contains a specific entry.
+   * Traverse the items in a binary search tree in preorder, inorder, or postorder.

For simplicity, we will insist that a binary search tree contain unique data. The following contract specifies the insertion and removal operations in more detail. The UML diagram for a class of binary search trees will be almost the same as the one for a class of binary trees, so we do not write one here.

| | ABSTRACT DATA TYPE: BINARY SEARCH TREE |
|---|---|
| Data | A finite number of objects in hierarchical order. |
| Operations | |
| PSEUDOCODE | DESCRIPTION |
| add(newEntry) | Task: Inserts newEntry into this binary search tree such that the properties of a binary search tree are maintained.
Input: newEntry is the data item to be inserted. Assumes the entries in the tree are distinct and differ from newEntry.
Output: True if the insertion is successful, or false if not. |
| remove(anEntry) | Task: Removes the given entry from this binary search tree such that the properties of a binary search tree are maintained.
Input: anEntry is the entry to remove.
Output: True if the removal is successful, or false if not. |
| | The methods isEmpty, getHeight, getNumberOfNodes, getRootData, clear, getEntry, contains, preorderTraverse, inorderTraverse, and postorderTraverse have the same specifications as for a binary tree. |

+   **Example.** If nameTree is any one of the binary search trees in Figures 15-13 and 15-14, and if their nodes contain strings, the statement
+   
+   `string name = nameTree.getEntry(nancy);`
+   
+   where nancy is a string variable containing "Nancy", locates the node containing "Nancy" and assigns its data to name. It doesn't matter which one of the four trees getEntry searches; the result will be the