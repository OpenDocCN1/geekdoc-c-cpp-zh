# 128

# 5.1 Minimum spanning trees

Input: An undirected graph $G = (V, E)$, with edge weights $w_e$.
Output: A tree $T = (V, E')$, with $E' \subseteq E$, minimizes
$weight(T) = \sum_{e \in E'} w_e$.

In the preceding example, the minimum spanning tree has a cost of 16:

![](bbox=[0.246, 0.213, 0.517, 0.316])

However, this is not the optimal solution. Can you spot another?

# 5.1.1 A greedy approach

Kruskal's minimum spanning tree algorithm starts with the empty graph and then selects edges from $E$ according to the following rule.

Repeatedly add the next lightest edge that produces a cycle.

In other words, it constructs the tree by edge by edge, apart from taking care to avoid cycles, simply picks whichever edge is cheapest at the moment. This is a greedy algorithm: every decision it makes is the one with the most obvious immediate advantage.

Figure 5.1 shows an example. We start with an empty graph and attempt to add edges in increasing order of weight (which are broken arbitrarily):

$B-C, C-D, B-D, C-F, D-F, E-F, A-D, A-B, C-E, A-C.$

The first two succeed, but the third, $B-D$, would produce a cycle if added. We ignore it and move along. The final result is a tree with cost 14, the minimum possible.

Figure 5.1 The minimum spanning tree found by Kruskal's algorithm.

![](bbox=[0.047, 0.773, 0.722, 0.891])