Question 4 Given the tree in Figure 15-4, what node or nodes are

+   - a. The tree's root?
+   - b. Parents?
+   - c. Children of the parents in part b of this question?
+   - d. Siblings?

# 15.1.2 The Height of Trees

Trees come in many shapes. For example, although the binary trees in Figure 15-5 all contain the same nodes, their structures are quite different. Although each of these trees has seven nodes, some are “taller” than others. The height of a tree is the number of nodes on the longest path from the root to a leaf. For example, the trees in Figure 15-5 have respective heights of 3, 5, 7, and 7. Many people’s intuitive notion of height would lead them to say that these trees have heights of 2, 4, 6, and 6. Indeed, many authors define height to agree with this intuition. However, the definition of height used in this book leads to a cleaner statement of many algorithms and properties of trees.

There are other equivalent ways to define the height of a tree. One way uses the following definition of the level of a node n:

# Level of a node

+   - If n is the root of T, it is at level 1.
+   - If n is not the root of T, its level is 1 greater than the level of its parent.

For example, in Figure 15-5a, node A is at level 1, node B is at level 2, and node D is at level 3.

The height of a tree T in terms of the levels of its nodes is defined as follows:

# Height of a tree in terms of levels

+   - If T is empty, its height is 0.
+   - If T is not empty, its height is equal to the maximum level of its nodes.

By applying this definition to the trees in Figure 15-5, you will find that their heights are, respectively, 3, 5, and 7, as was stated earlier.

# FIGURE 15-5 Binary trees with the same nodes but different heights

![](bbox=[0.18, 0.58, 0.92, 0.76])

# Recursive definition of height

For binary trees, it is often convenient to use an equivalent recursive definition of height:

+   - If T is empty, its height is 0.
+   - If T is a nonempty binary tree, then because T is of the form

![](bbox=[0.4, 0.87, 0.55, 0.92])