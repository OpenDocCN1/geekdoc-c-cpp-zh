super source $ss$ and a super sink $st$. Connect $ss$ with all $s$ with infinite capacity and also connect $tt$ with all $t$ with infinite capacity, then run Edmonds Karp’s algorithm as per normal.

# Max Flow with Vertex Capacities

![](bbox=[0.176, 0.158, 0.84, 0.244])

Figure 4.23: Vertex Splitting Technique

We can also have a Max Flow variant where capacities are not just defined along the edges but also on the vertices. To solve this variant, we can use the vertex splitting technique. A graph with a vertex weight can be converted into a more familiar graph without a vertex weight by splitting the vertex $v$ to $v_{out}$ and $v_{in}$, reassigning incoming edges to $v_{out}$/outgoing edges to $v_{in}$, and putting the original vertex $v$’s weight as the weight of edge $(v_{out}, v_{in})$. For details, see Figure 4.23. Then run Edmonds Karp’s algorithm as per normal.

# Max Independent Paths

The problem of finding the maximum number of independent paths from source $s$ to sink $t$ can be reduced to the Max Flow problem. Two paths are said to be independent if they do not share any vertex apart from $s$ and $t$ (vertex-disjoint). Solution: construct a flow network $N = (V, E)$ from $G$ with vertex capacities, where $N$ is the carbon copy of $G$ except that the capacity of each $v \in V$ is 1 (i.e. each vertex can only be used once) and the capacity of each $e \in E$ is also 1 (i.e. each edge can only be used once too). Then run Edmonds Karp’s algorithm as per normal.

# Max Edge-Disjoint Paths

Finding the maximum number of edge-disjoint paths from $s$ to $t$ is similar to finding max independent paths. The only difference is that this time we do not have any vertex capacity (i.e. two edge-disjoint paths can still share the same vertex). See Figure 4.24 for a comparison between independent paths and edge-disjoint paths from $s = 1$ to $t = 7$.

![](bbox=[0.122, 0.696, 0.885, 0.84])

Figure 4.24: Comparison Between Max Independent Paths versus Max Edge-Disjoint Paths