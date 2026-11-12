The basic idea of the algorithm is simple:

```
// Sorts the integers in an array into ascending order.
treeSort(anArray: array, n: integer)
   Insert anArray's entries into a binary search tree bst
   Traverse bst in inorder. As you visit bst's nodes, copy their data items into successive
   locations of anArray
```

An inorder traversal of the binary search tree bst visits the integers in bst's nodes in ascending order.

A tree sort can be quite efficient. As Figure 15-17 in Chapter 15 indicates, each insertion into a binary search tree requires O(log n) operations in the average case and O(n) operations in the worst case. Thus, tree sort's n insertions require O(n x log n) operations in the average case and O(n^2) operations in the worst case. The traversal of the tree involves one copy operation for each of the n entries and so is O(n). Because O(n) is less than O(n x log n) and O(n^2), tree sort in the average case is O(n x log n) and O(n^2) in the worst case.

Tree sort uses a binary search tree bst

Tree sort is O(n x log n) in the average case and O(n^2) in the worst case

Question 10 Trace the tree sort algorithm as it sorts the following array into ascending order: 20 80 40 20 50 60 30.

# 16.6 General Trees

This chapter ends with a brief discussion of general trees and their relationship to binary trees. Consider the general tree in Figure 16-18. The three children B, C, and D of node A, for example, are siblings. The leftmost child B is the oldest child, or first child, of A, as mentioned in Section 15.1 of Chapter 15. One way to implement this tree uses the BinaryNode objects that we used for a link-based binary tree. That is, each node has two pointers: The left pointer points to the node's oldest child and the right pointer points to the node's next sibling. Thus, you can use the data structure in Figure 16-19a to implement the tree in Figure 16-18. Notice that the structure in Figure 16-19a also represents the binary tree pictured in Figure 16-19b.

Recall from Chapter 15 that an n-ary tree is a generalization of a binary tree whose nodes each can have no more than n children. The tree in Figure 16-18 could be an n-ary tree with n = 3 instead of a general tree. You can, of course, use the implementation just described for an n-ary tree. However, because you know the maximum number of children for each node, you can let each node point directly to its children. Figure 16-20 illustrates such a representation for the tree in Figure 16-18. This tree is shorter than the tree in Figure 16-19b.

FIGURE 16-18 A general tree

![](bbox=[0.25, 0.73, 0.75, 0.9])