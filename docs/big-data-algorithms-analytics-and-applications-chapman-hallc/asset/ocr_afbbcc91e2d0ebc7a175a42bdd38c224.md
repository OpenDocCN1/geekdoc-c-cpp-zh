+   1. Distance defined as (D_max − D_min)/D_min, where D_max and D_min are the points with the farthest and least distance from a target point, decreases with increasing dimensionality. Setting 0 ≤ p ≤ 1 has been proposed in References 37 and 38 to provide more meaningful distance measures.
+   2. Clusters are intended to group objects based on attribute values, but some of the large number of attributes may not be meaningful for a given cluster. This is known as the local feature relevance problem: Different clusters might be found in different subspaces.
+   3. Subsets of attributes might be correlated; hence, clusters might exist in arbitrarily oriented affine subspaces (in affine geometry, the coordinates are not necessarily orthonormal).
+   4. Problem 4 is similar to problem 3 in that there may be some correlations among subsets of attributes.

D(u, v) = ( Σ_{i=1}^{n} |u_i - v_i|^p )^{1/p} . (3.6)

p = 1 yields the Manhattan distance and p = 2 the Euclidean distance.

Given n points and k clusters, the number of possible clusters is a Stirling number of the second kind defined as follows:

S(n, k) = n/k = 1/k! Σ_{t=0}^{k} (-1)^t / t! (k - t)^n .

S(n, 1) = S(n, n) = 1, S(4, 2) = 7 because there are seven ways to partition four objects, a, b, c, d, into two groups: (a)(bcd), (b)(acd), (c)(abd), (d)(abc), (ab)(cd), (ac)(bd), (ad)(bc)

Recursion can be used to compute S(n, k) = k S(n - 1, k) + S(n - 1, k - 1), 1 ≤ k < n, and to show that S(n, k) increases rapidly, for example, S(10, 5) = 42525. Cluster analysis can be classified into the following methods.

# 3.3.1 Partitioning Methods

Partition n data points based on their distances from each other into k clusters. Each cluster has at least one point, and each point belongs to one cluster, unless a fuzzy clustering algorithm is considered, in which case the allocation of data points to clusters is