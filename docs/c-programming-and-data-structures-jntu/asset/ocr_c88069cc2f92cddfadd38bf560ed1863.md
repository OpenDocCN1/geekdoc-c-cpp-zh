# Chapter 16

# Binary Trees and Graphs

# 16.1 BINARY TREES—REPRESENTATION AND TERMINOLOGY

The data structure of type tree comes in many forms. However, the binary tree is a bit special, because when they are in the sorted form, they facilitate quick search, insertion and deletion. Each item in a tree has two links: one to a left member, and another to a right member. This concept is shown in Fig. 16.1.

![](bbox=[0.3, 0.5, 0.75, 0.7])

Fig. 16.1 Binary tree

In this figure, d is the root of the tree. Each data item (a through g) is called as a node. Any portion of a tree (e.g. a-b-c) is called as a sub-tree. A node that does not have any sub-tree is called as a terminal node. For example, a, c, e and g are terminal nodes, whereas b, d and f are not. The height of the tree is the number of the vertical node positions. In the sample tree just shown, the height is 3. Accessing a tree is called as the process of tree traversal.

Items of a tree can be accessed, inserted or deleted in any order. Interestingly, each sub-tree of a tree is itself a tree. Therefore, a tree is a recursive (i.e. self-repeating) data structure, and recursive programming techniques are popularly used with trees. Of course, tree-related programming need not always be recursive. Non-recursive tree programming is also possible, but is much harder to code and understand, as compared to the recursive version.