![](bbox=[0.07, 0.08, 0.72, 0.18])

Figure 12.50 The plane partitioned by a 2-d tree after the insertion of \(p_1 = (53, 14)\), \(p_2 = (27, 28)\), \(p_3 = (30, 11)\), \(p_4 = (67, 51)\), \(p_5 = (70, 3)\)

12.32 When viewed graphically, each node in a 2-d tree partitions the plane into regions. For instance, Figure 12.50 shows the first five insertions into the 2-d tree in Figure 12.39. The first insertion, of \(p_1\), splits the plane into a left and a right part. The second insertion, of \(p_2\), splits the left part into a top part and a bottom part, and so on.
a. For a given set of \(N\) items, does the order of insertion affect the final partition?
b. If two different insertion sequences result in the same tree, is the same partition produced?
c. Give a formula for the number of regions that result from the partition after \(N\) insertions?
d. Show the final partition for the 2-d tree in Figure 12.39.

12.33 An alternative to the 2-d tree is the quad tree. Figure 12.51 shows how a plane is partitioned by a quad tree. Initially, we have a region (which is often a square, but need not be). Each region may store one point. If a second point is inserted into a region, then the region is split into four equal-sized quadrants (northeast, southeast, southwest, and northwest). If this places the points in different quadrants (as when \(p_2\) is inserted), we are done; otherwise, we continue splitting recursively (as is done when \(p_5\) is inserted).
a. For a given set of \(N\) items, does the order of insertion affect the final partition?
b. Show the final partition if the same elements that were in the 2-d tree in Figure 12.39 are inserted into the quad tree.

12.34 A tree data structure can store the quad tree. We maintain the bounds of the original region. The tree root represents the original region. Each node is either a leaf that stores an inserted item, or has exactly four children, representing four quadrants. To perform a search, we begin at the root and repeatedly branch to an appropriate quadrant until a leaf (or null ptr) is reached.

![](bbox=[0.07, 0.76, 0.72, 0.86])

Figure 12.51 The plane partitioned by a quad tree after the insertion of \(p_1 = (53, 14)\), \(p_2 = (27, 28)\), \(p_3 = (30, 11)\), \(p_4 = (67, 51)\), \(p_5 = (70, 3)\)