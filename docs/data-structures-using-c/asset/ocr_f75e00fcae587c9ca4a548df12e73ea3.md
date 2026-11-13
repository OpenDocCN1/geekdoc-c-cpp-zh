# Dynamic Tree Tables

A dynamic tree table is used when symbols are not known in advance but are inserted as they come and deleted if not required. Dynamic keyed tables are those that are built on-the-fly. The keys have no history associated with their use. The dynamically built tree that is a balanced BST is the best choice.

Let us now look into each of these trees in detail.

# 10.2 OPTIMAL BINARY SEARCH TREE

Before we study OBSTs, let us revise BSTs. A BST is one of the most important data structures in computer science. When arrays are used to store ordered data, we use the very efficient searching technique, that is, binary search. However, its insertion and deletion algorithms are inefficient as they require shifting of data in the array. An alternative is to use a linked list to store ordered data, which although provides efficient insertion and deletion algorithms, its sequential searching algorithm is inefficient. Therefore, a BST is the only data structure left that not only has an efficient searching algorithm but also efficient insertion and deletion algorithms.

A BST can be defined as a key-based tree with the following properties:

+   1. Every element has a key, and no two elements have the same key (i.e., keys are unique).
+   2. The keys (if any) in the left subtree are smaller than the key in the root.
+   3. The keys (if any) in the right subtree are greater than the key in the root.
+   4. Each subtree in itself is a BST.

A BST has a few problems which are to be overcome. Consider the BST shown in Fig. 10.1.

![](bbox=[0.386, 0.633, 0.723, 0.763])

Fig. 10.1 Sample binary search tree

The inorder traversal produces 10, 20, 22, 25, 27, 30, 35. For the same set of keys, depending on their sequence of arrival, the other two search trees can be constructed as in Fig. 10.2.