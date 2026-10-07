# 7.2 Flows in networks

optimality of the maximum flow. This isn't just a lucky property of our oil network; such a cut always exists.

# Max-flow min-cut theorem:

The size of the maximum flow in a network equals the capacity of the smallest (s, t)-cut.

Moreover, our algorithm automatically finds this cut as a by-product!

Let's see why this is true. Suppose f is the final flow when the algorithm terminates. We know that t is no longer reachable from s in the residual network G^f. Let L the nodes that are reachable from s in G^f, and R = V - L be the rest of the nodes. Then (L, R) is a cut in the graph G:

![](bbox=[0.213, 0.308, 0.538, 0.433])

We claim that

size(f) = capacity(L, R).

To see this, observe by the way L is defined, any edge going from L to R must be at capacity (in the current flow), and any edge from R to L must have zero flow. (So, in the figure, f_e = c_e and f_e = 0.) Therefore the net flow across (L, R) is exactly the capacity of the cut.

# 7.2.5 Efficiency

Each iteration of our maximum-flow algorithm is efficient, running O(|E|) time if a depth-first or breadth-first search is used to find an s - t path. But how many iterations are there?

Suppose all edges in the original network have integer capacities ≤ C. Then an inductive argument shows that on each iteration of the algorithm, the flow is always an integer and increases by an integer. Therefore, if the maximum flow is at most C|E| (why?), it follows that the number of iterations is at most This is hardly a rewarding bound: what if C is in the millions?

We examine this issue further in Exercise 7.31. It turns out that it is possible to construct bad examples in the way the number of iterations is proportional to C, if s - t paths are not carefully chosen. If paths are chosen in a sensible manner—in particular, by using a breadth-first search, which finds the path with the fewest edges—the number of iterations is at O(|V|·|E| no matter what the capacities are. This latter gives an overall running time of O(|V||E²) for maximum flow.