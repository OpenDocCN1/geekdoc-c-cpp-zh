+   4.39 Write a general-purpose tree-drawing program that will convert a tree into the following graph-assembler instructions:
+   a. Circle(X, Y)
+   b. DrawLine(i, j)
+   The first instruction draws a circle at (X, Y), and the second instruction connects the ith circle to the jth circle (circles are numbered in the order drawn). You should either make this a program and define some sort of input language or make this a function that can be called from any program. What is the running time of your routine?

4.40 Write a routine to list out the nodes of a binary tree in level-order. List the root, then nodes at depth 1, followed by nodes at depth 2, and so on. You must do this in linear time. Prove your time bound.

+   4.41 * a. Write a routine to perform insertion into a B-tree.
+   * b. Write a routine to perform deletion from a B-tree. When an item is deleted, is it necessary to update information in the internal nodes?
+   * c. Modify your insertion routine so that if an attempt is made to add into a node that already has M entries, a search is performed for a sibling with less than M children before the node is split.

4.42 A B+-tree of order M is a B-tree in which each interior node has between 2M/3 and M children. Describe a method to perform insertion into a B+-tree.

4.43 Show how the tree in Figure 4.77 is represented using a child/sibling link implementation.

4.44 Write a procedure to traverse a tree stored with child/sibling links.

4.45 Two binary trees are similar if they are both empty or both nonempty and have similar left and right subtrees. Write a function to decide whether two binary trees are similar. What is the running time of your function?

+   4.46 Two trees, T1 and T2, are isomorphic if T1 can be transformed into T2 by swapping left and right children of (some of the) nodes in T1. For instance, the two trees in Figure 4.78 are isomorphic because they are the same if the children of A, B, and G, but not the other nodes, are swapped.
+   a. Give a polynomial time algorithm to decide if two trees are isomorphic.

![](bbox=[0.07, 0.73, 0.85, 0.88])

Figure 4.77 Tree for Exercise 4.43