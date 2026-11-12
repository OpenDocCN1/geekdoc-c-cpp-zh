Insert 35, 34, and 33. Each of these insertions is similar to the previous ones. Figure 19-11 shows the tree after the three insertions.

# FIGURE 19-11 The tree after the insertion of 35, 34, and 33 into the tree in Figure 19-10d

![](bbox=[0.07, 0.19, 0.78, 0.34])

> Question 1 To be sure that you fully understand the insertion algorithm, insert 32 into the 2-3 tree in Figure 19-11. The result should be the tree shown in Figure 19-6b. Once again, compare this tree with the binary search tree shown in Figure 19-6a and notice the dramatic advantage of the 2-3 tree's insertion strategy.

The insertion algorithm. Let's consider the general strategy for inserting an item into a 2-3 tree. To begin, you locate the leaf at which the search for the new item would terminate. If the leaf does not contain two items, you insert the new item into the leaf, and you are done. However, if the leaf already contains two items, you must split it into two nodes, n1 and n2. As Figure 19-12 illustrates, you place the smallest item S into n1, place the largest item L into n2, and try to move the middle item M up to the original leaf's parent. If the parent has room for a new item — as is true here — nodes n1 and n2 become children of the parent, and you are finished. The parent now has only three children and contains two items.

> When a leaf would contain three items, split it into two nodes

# FIGURE 19-12 Splitting a leaf in a 2-3 tree when the leaf is a (a) left child; (b) right child

![](bbox=[0.07, 0.69, 0.78, 0.93])