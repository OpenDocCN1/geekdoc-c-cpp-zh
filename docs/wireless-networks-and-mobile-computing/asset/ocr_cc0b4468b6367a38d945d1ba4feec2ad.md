The following theorem analyzes the time complexity of each iteration of the above heuristic algorithm.

**Theorem 24.** *The worst case time complexity of an iteration is* $O(n + k\log k)$.

*Proof.* The factors involved in this analysis are as follows:

+   - Computing $VOR(P)$ can be done in $O(k\log k)$ time [3].
+   - $VOR(P)$ splits the convex polygonal region $\Pi$ into $k$ closed cells. Each edge of $VOR(P)$ appears in at most two cells. As the number of edges of the region $\Pi$ is $n$, identifying these $k$ cells requires $O(n+k)$ time.
+   - Computing the minimum enclosing circle of a convex polygon needs time linear in its number of edges [4]. Thus, computing $\{C_i, i = 1, 2, \ldots, k\}$, needs $O(n+k)$ time.

The number of iterations needed to reach local optima from an initial configuration is reasonably small. The overall time complexity depends on the number of times we apply the refinement step.

# 7.4 Experimental Results

An exhaustive experiment has been performed with several convex shapes of region $\Pi$ and with different values of $k$. For a given initial placement of $P$ the value of $\rho$ is decreased at each iteration. As the process reaches local minima, the quality of the result depends on the initial choice of the positions of $P$. Studies have been made of random distribution of $P$. In an optimal solution, the distribution of points is very regular. To get the best possible results, the initial distribution of the points was carefully chosen. Thus, while performing the experiment with a unit square region,