# Exercises

7.29. Hollywood. A film producer is seeking and investors for his new movie. There are $n$ available actors; actor $i$ charges $s_i$ dollars. For funding, there are $m$ available investors; investor $j$ provides $p_j$, but only on the condition that certain actors $L_i \subseteq \{1, \dots, n\}$ are included in the cast (*all* of these actors $L_i$ must be chosen to receive funding from investor $j$).

The producer's profit is the sum of the payments from investors minus the payments to actors. The goal is to maximize this profit.

+   (a) Express this problem as an integer linear program in which the variables take on values [0, 1].

+   (b) Now relax this to a linear program, and show that there must in fact an integral optimal solution (as is the case, for example, with maximum flow and bipartite matching).

7.30. Hall's theorem. Returning to the matchmaking scenario of Section 7.3, we have a bipartite graph with boys on the left and an equal number of girls on the right. Hall's theorem says that there is a perfect matching if and only if every subset $S$ of boys is connected to at least $|S|$ girls.

Prove this theorem. (Hint: The max-flow min-cut theorem should be helpful.)

7.31. Consider the following simple network with edge capacities as shown.

![](bbox=[0.273, 0.465, 0.526, 0.581])

+   (a) Show that, if the Ford-Fulkerson algorithm is run on this graph, a careless choice of updates might cause it to take 1000 iterations. Imagine if the capacities were a minimum instead of 1000!

We will now find a strategy for choosing paths under which the algorithm is guaranteed to terminate in a reasonable number of iterations.

Consider an arbitrary directed network $G=(V, E), s, t, \{c_{ij}\}$ in which we want to find the maximum flow. For simplicity assume all edge capacities are at least 1, and define the capacity of an $s-t$ path to be the smallest capacity of its constituent edges. The *fattest path* from $s$ to $t$ is the path with the most capacity.

+   (b) Show that the fattest $s-t$ path can be computed in a graph using Dijkstra's algorithm.

+   (c) Show that the maximum flow in $G$ is the sum of individual flows along at most $|E|$ paths from $s$ to $t$.

+   (d) Now show that if we always increase flow along the fattest path in the residual graph, then the Ford-Fulkerson algorithm will terminate in at