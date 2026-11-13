Can you work out the order of the output numbers for the in-order and post-order traversals on an example such as Figure 10.5 on page 484? You'll be asked to work that out in Self-Test Exercise 15 at the end of this section.

# Printing the Data from a Tree's Node

In debugging a program, the nodes of a tree are generally printed using a pre-order traversal, printing each parent prior to its children. For example, consider the small tree shown here, along with the output from the pre-order traversal:

+   14
+   17
+   9
+   13
+   53
+   11
+   4
+   99

![](bbox=[0.45, 0.3, 0.65, 0.44])

There are two items that will make the output easier to read. The first trick is to print some indication when a node is a leaf or when a node has only one child. The second trick is to indent each number according to its depth in the tree. Each number will have an indentation of four times the depth of the node, as shown here:

```
14
   17
      9
         [Empty]
         13 [leaf]
      53 [leaf]
   11
      4 [leaf]
      99 [leaf]
```

Each leaf node has the word [leaf] printed after the data. Each nonleaf node has its two children printed below it with an extra four spaces of indentation. For example, the node containing 17 has a left child (containing 9) and a right child (containing 53). Notice that the node containing 9 has only a right child. In the spot where the left child would be printed if it existed is the word [Empty].

The function to carry out this kind of printing is a pre-order traversal with one extra parameter to carry information about the depth of each node. The implementation is shown at the top of the next page.