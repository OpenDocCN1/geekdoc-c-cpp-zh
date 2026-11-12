**Question 7** Why does a node in a red-black tree require less memory than a node in a 2-3-4 tree?

# 19.4.1 Searching and Traversing a Red-Black Tree

Because a red-black tree is a binary search tree, you can search and traverse it by using the algorithms for a binary search tree. You simply ignore the color of the pointers.

# 19.4.2 Inserting into and Removing from a Red-Black Tree

Because a red-black tree actually represents a 2-3-4 tree, you simply need to adjust the 2-3-4 insertion algorithms to accommodate the red-black representation. Recall that while searching a 2-3-4 tree, you split each 4-node that you encounter, so it is sufficient to reformulate that process in terms of the red-black representation. For example, Figure 19-31a shows the red-black representation of a 4-node. Thus, to identify a 4-node in its red-black form, you look for a node that has two red pointers.

Suppose that the 4-node is the root of the 2-3-4 tree. Figure 19-28 shows how to split the root into 2-nodes. By comparing this figure with Figure 19-31a, you see that to perform an equivalent operation on a red-black tree, you simply change the color of its root’s pointers to black, as Figure 19-33 illustrates.

# FIGURE 19-33 Splitting a red-black representation of a 4-node that is the root

![](bbox=[0.35, 0.49, 0.65, 0.58])

+   - Splitting the equivalent of a 4-node requires only simple color changes
+   - Pointer changes called rotations result in a shorter tree

Figure 19-29 shows how to split a 4-node whose parent is a 2-node. If you reformulate this figure by using the red-black notation given in Figure 19-31, you get Figure 19-34. Notice that this case also requires only color changes within the red-black tree.

Finally, Figure 19-30 shows how to split a 4-node whose parent is a 3-node. Figure 19-35 shows this process for a red-black tree, using the transformations that Figure 19-31 describes. Note that each of the configurations before the split in Figure 19-30 has two red-black representations, as Figure 19-35 illustrates. As you can see, each pair of representations transforms into the same red-black representation. Of the six possibilities given in Figure 19-35, only two require simple color changes. The others also require changes to the pointers themselves. These pointer changes, which are called rotations, result in a shorter tree.

The removal algorithm is derived in an analogous fashion from the 2-3-4 tree removal algorithm. Because insertion and removal operations on a red-black tree frequently require only color changes, they are more efficient than the corresponding operations on a 2-3-4 tree.

Exercise 11 asks you to complete the details of the insertion and removal algorithms.

**Question 8** What red-black tree represents the 2-3-4 tree in Figure 19-27a?