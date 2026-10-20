Now run your simulation for 720 minutes and answer each of the following:

+   a) What is the maximum number of customers in the queue at any time?
+   b) What is the longest wait any one customer experiences?
+   c) What happens if the arrival interval is changed from 1 to 4 minutes to 1 to 3 minutes?

# 22.16 (Allowing Duplicates in a Binary Tree) Modify Figs. 22.17 and 22.18 to allow the binary tree to contain duplicates.

# 22.17 (Processing a Binary Search Tree of Strings) Write a program based on the program of Figs. 22.17 and 22.18 that inputs a line of text, tokenizes it into separate words, inserts the words in a binary search tree and prints the inorder, preorder and postorder traversals of the tree.

# 22.18 (Duplicate Elimination) In this chapter, we saw that duplicate elimination is straightforward when creating a binary search tree. Describe how you’d perform duplicate elimination when using only a one-dimensional array. Compare the performance of array-based duplicate elimination with the performance of binary-search-tree-based duplicate elimination.

# 22.19 (Depth of a Binary Tree) Modify Figs. 22.17 and 22.18 so the Tree class provides a method getDepth that determines how many levels are in the tree. Test the method in an application that inserts 20 random integers in a Tree.

# 22.20 (Recursively Print a List Backward) Modify the List<T> class of Fig. 22.3 to include method printListBackward that recursively outputs the items in a linked-list object in reverse order. Write a test program that creates a list of integers and prints the list in reverse order.

# 22.21 (Recursively Search a List) Modify the List<T> class of Fig. 22.3 to include method search that recursively searches a linked-list object for a specified value. The method should return a reference to the value if it’s found; otherwise, it should return null. Use your method in a test program that creates a list of integers. The program should prompt the user for a value to locate in the list.

# 22.22 (Binary Tree Delete) In this exercise, we discuss deleting items from binary search trees. The deletion algorithm is not as straightforward as the insertion algorithm. Three cases are encountered when deleting an item—the item is contained in a leaf node (i.e., it has no children), or in a node that has one child or in a node that has two children.

If the item to be deleted is contained in a leaf node, the node is deleted and the reference in the parent node is set to null.

If the item to be deleted is contained in a node with one child, the reference in the parent node is set to reference the child node and the node containing the data item is deleted. This causes the child node to take the place of the deleted node in the tree.

The last case is the most difficult. When a node with two children is deleted, another node in the tree must take its place. However, the reference in the parent node cannot simply be assigned to reference one of the children of the node to be deleted. In most cases, the resulting binary search tree would not embody the following characteristic of binary search trees (with no duplicate values): The values in any left subtree are less than the value in the parent node, and the values in any right subtree are greater than the value in the parent node.

Which node is used as a replacement node to maintain this characteristic? It’s either the node containing the largest value in the tree less than the value in the node being deleted, or the node containing the smallest value in the tree greater than the value in the node being deleted. Let’s consider the node with the smaller value. In a binary search tree, the largest value less than a parent’s value is located in the left subtree of the parent node and is guaranteed to be contained in the rightmost node of the subtree. This node is located by walking down the left subtree to the right until the reference to the right child of the current node is null. We’re now referencing the replacement node, which is either a leaf node or a node with one child to its left. If the replacement node is a leaf node, the steps to perform the deletion are as follows:

+   a) Store the reference to the node to be deleted in a temporary reference variable.