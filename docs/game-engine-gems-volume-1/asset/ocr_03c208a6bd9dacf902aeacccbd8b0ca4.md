# Refinement

After all triangles have been assigned to partitions, the last partition is, on average, half the size of the others. Even if this is acceptable, you might want to perform a refinement on the partitions. You can typically run the refinement multiple times to level out some of the partitions and reduce the total size of the solution. To refine, follow these steps for each partition:

+   1. Determine if any triangle can be moved from partition A to partition B, where A loses some vertices and B gains none. This is a clear win for memory and performance, but may distort bounding volumes or cause the triangle counts across partitions to become unbalanced. This is demonstrated in step 14 of the graphical walkthrough at the end of this gem.

+   2. Determine if any triangle can move from partition A to partition B, where B has fewer triangles, even if the number of vertices remains the same in both partitions. This balances the triangle count between partitions, but can be done to improve the bounding volume or triangle count balance.

+   3. As a last resort, determine if any one vertex can be moved from partition A to partition B, possibly moving several triangles to B in the process, so that A has fewer vertices and triangles, and B has more. This is particularly useful when filling out the final partition, because the final partition is on average half the size of the others.

[1]Least connected, in this context, means the unassigned triangle that has fewest shared vertices with other unassigned triangles. This is a dynamic property of a triangle during partitioning, and cannot be precomputed.

[2]Related, as defined for partitioning, is the statement that vertex data within a partition could be shared with adjacent unassigned triangles. This property forms the basis of candidate triangles for