# REVIEW EXERCISES

R16.1 What are all possible shapes of trees of height h with one leaf? Of height 2 with k leaves?

R16.2 Describe a recursive algorithm for finding the maximum number of siblings in a tree.

R16.3 Describe a recursive algorithm for finding the total path length of a tree. The total path length is the sum of the lengths of all paths from the root to the leaves. (The length of a path is the number of nodes on the path.) What is the efficiency of your algorithm?

R16.4 Show that a binary tree with l leaves has at least l − 1 interior nodes, and exactly l − 1 interior nodes if all of them have two children.

R16.5 What is the difference between a binary tree and a binary search tree? Give examples of each.

R16.6 What is the difference between a balanced tree and an unbalanced tree? Give examples of each.

R16.7 The following elements are inserted into a binary search tree. Make a drawing that shows the resulting tree after each insertion.

+   - Adam
+   - Eve
+   - Romeo
+   - Juliet
+   - Tom
+   - Diana
+   - Harry

R16.8 Insert the elements of Exercise R16.7 in opposite order. Then determine how the BinarySearchTree.print function from Section 16.4.1 prints out both the tree from Exercise R16.7 and this tree. Explain how the printouts are related.

R16.9 Consider the following tree. In which order are the nodes printed by the BinarySearchTree.print function from Section 16.4.1? The numbers identify the nodes. The data stored in the nodes is not shown.

![](bbox=[0.55, 0.6, 0.95, 0.85])

R16.10 Design an algorithm for finding the kth element (in sort order) of a binary search tree. How efficient is your algorithm?

R16.11 Design an O(log n) algorithm for finding the kth element in a binary search tree, provided that each node has a data member containing the size of the subtree. Also describe how these data members can be maintained by the insertion and removal operations without affecting their big-Oh efficiency.