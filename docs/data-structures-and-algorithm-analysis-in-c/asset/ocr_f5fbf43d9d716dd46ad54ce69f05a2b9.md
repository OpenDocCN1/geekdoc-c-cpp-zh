![](bbox=[0.214, 0.102, 0.846, 0.172])

# Figure 8.1 Eight elements, initially in different sets

easy, because the only information we will need is a parent link. The name of a set is given by the node at the root. Since only the name of the parent is required, we can assume that this tree is stored implicitly in an array: Each entry s[i] in the array represents the parent of element i. If i is a root, then s[i] = -1. In the forest in Figure 8.1, s[i] = -1 for 0 <= i < 8. As with binary heaps, we will draw the trees explicitly, with the understanding that an array is being used. Figure 8.1 shows the explicit representation. We will draw the root's parent link vertically for convenience.

To perform a union of two sets, we merge the two trees by making the parent link of one tree's root link to the root node of the other tree. It should be clear that this operation takes constant time. Figures 8.2, 8.3, and 8.4 represent the forest after each of union(4,5), union(6,7), union(4,6), where we have adopted the convention that the new root after the union(x, y) is x. The implicit representation of the last forest is shown in Figure 8.5.

A find(x) on element x is performed by returning the root of the tree containing x. The time to perform this operation is proportional to the depth of the node representing x, assuming, of course, that we can find the node representing x in constant time. Using the strategy above, it is possible to create a tree of depth N - 1, so the worst-case running

![](bbox=[0.214, 0.575, 0.846, 0.675])

# Figure 8.2 After union(4,5)

![](bbox=[0.214, 0.755, 0.846, 0.885])

# Figure 8.3 After union(6,7)