need to traverse the entire tree. At every node, we get a hint regarding which sub-tree to search in. For example, in the given tree, if we have to search for 29, then we know that we have to scan only the left sub-tree. If the value is present in the tree, it will only be in the left sub-tree, as 29 is smaller than 39 (the root node’s value). The left sub-tree has a root node with the value 27. Since 29 is greater than 27, we will move to the right sub-tree, where we will find the element. Thus, the average running time of a search operation is O(log n), as at every step, we eliminate half of the sub-tree from the search process. Due to its efficiency in searching elements, binary search trees are widely used in dictionary problems where the code always inserts and searches the elements that are indexed by some key value.

Binary search trees also speed up the insertion and deletion operations. The tree has a speed advantage when the data in the structure changes rapidly.

Binary search trees are considered to be efficient data structures especially when compared with sorted linear arrays and linked lists. In a sorted array, searching can be done in O(log n) time, but insertions and deletions are quite expensive. In contrast, inserting and deleting elements in a linked list is easier, but searching for an element is done in O(n) time. However, in the worst case, a binary search tree will take O(n) time to search for an element. The worst case could occur when the tree is a linear chain of nodes as given in Fig. 10.2.

![](bbox=[0.1, 0.35, 0.4, 0.48])

Figure 10.2 (a) Left skewed, and (b) right skewed binary search trees

+   To summarize, a binary search tree is a binary tree with the following properties:
+   * The left sub-tree of a node n contains values that are less than n’s value.
+   * The right sub-tree of a node n contains values that are greater than n’s value.
+   * Both the left and the right binary trees also satisfy these properties and, thus, are binary search trees.

# Example 10.1 State whether the binary trees in Fig. 10.3 are binary search trees or not.

# Solution

![](bbox=[0.3, 0.59, 0.7, 0.68])

Figure 10.3 Binary trees

# Example 10.2 Create a binary search tree using the following data elements: 45, 39, 56, 12, 34, 78, 32, 10, 89, 54, 67, 81

# Solution

![](bbox=[0.14, 0.77, 0.88, 0.93])