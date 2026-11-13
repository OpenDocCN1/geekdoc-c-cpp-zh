increase, the potential change is at most O(logN) = T. Adding the actual time and potential change gives the O(logN) amortized bound for deleteMin.

Finally, for the decreaseKey operation, let C be the number of cascading cuts. The actual cost of a decreaseKey is C + 1, which is the total number of cuts performed. The first (noncascading) cut creates a new tree and thus increases the potential by 1. Each cascading cut creates a new tree but converts a marked node to an unmarked (root) node, for a net loss of one unit per cascading cut. The last cut also can convert an unmarked node (in Fig. 11.20 it is node 5) into a marked node, thus increasing the potential by 2. The total change in potential is thus at most 3 - C. Adding the actual time and the potential change gives a total of 4, which is O(1)).

# 11.5 Splay Trees

As a final example, we analyze the running time of splay trees. Recall, from Chapter 4, that after an access of some item X is performed, a splaying step moves X to the root by a series of three operations: zig, zig-zag, and zig-zig. These tree rotations are shown in Figure 11.21. We adopt the convention that if a tree rotation is being performed at node X, then prior to the rotation, P is its parent and (if X is not the child of the root) G is its grandparent.

Recall that the time required for any tree operation on node X is proportional to the number of nodes on the path from the root to X. If we count each zig operation as one

![](bbox=[0.08, 0.52, 0.8, 0.88])

Figure 11.21 zig, zig-zag, and zig-zig operations; each has a symmetric case (not shown)