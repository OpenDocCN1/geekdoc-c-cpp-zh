![](bbox=[0.15, 0.08, 0.85, 0.35])

# Figure 10.30 P partitioned into $P_L$ and $P_R$; shortest distances are shown

in Figure 10.32 implements this strategy, assuming the C++ convention that the points are indexed starting at 0.

In the worst case, all the points could be in the strip, so this strategy does not always work in linear time. We can improve this algorithm with the following observation: The y coordinates of the two points that define $d_C$ can differ by at most $\delta$. Otherwise, $d_C > \delta$. Suppose that the points in the strip are sorted by their y coordinates. Therefore, if $p_1$ and $p_j$'s

![](bbox=[0.15, 0.6, 0.85, 0.88])

# Figure 10.31 Two-lane strip, containing all points considered for $d_C$ strip