and

$c_{i,j} \neq c_{k,j}, \quad 1 \le k < i,$

and

$c_{i,j} \neq c_{k,i}, \quad 1 \le k < i.$

This completes the algorithm for nonoriented graphs.

Let us now estimate the complexity of the algorithm, namely, the amount of storage and computation time it requires. Clearly, the storage requirement is proportional to $N^2$, the number of elements in $A$. The number of calculations required is proportional to $N^2 \bar{e}$, where $\bar{e}$ is the average number of nonzero elements per row.

The reason for these rather large complexity estimates is that valuable resources are wasted on the zero elements in $A$. More precisely, the drawback is not in the algorithm but rather in the implementation. Indeed, when $\bar{e}$ is much smaller than $N$, $A$ is sparse, namely, most of its elements vanish. It is thus pointless to store the zero elements in $A$ or use them in the above algorithm. It makes more sense to store only the nonzero elements in $A$, using flexible data structures. The above algorithm can then be implemented much more efficiently, because only nonzero elements are used.

In what follows, we consider a suitable implementation for the sparse matrix $A$ and the coloring algorithm. When talking about complexity, we often omit the words "proportional to" and assume that the complexity estimates are up to multiplication by a constant independent of $N$ or $\bar{e}$.

# 4.27 Downward Implementation

The above implementation of the coloring algorithm may be viewed as an "upward" implementation, in which the basic objects are implemented first and then used to implement more complex objects (Figure 4.1). Indeed, the basic objects in the graphs, the nodes, are stored in an $N$-dimensional array. This way, the $i$th entry in the array may contain information about the $i$th node, such as its geometric location. The index $1 \le i \le N$ is then used to refer to the $i$th node; in fact, it can be considered as the "virtual address" of this node in the array of nodes. This virtual address may be different from the physical address of the

![](bbox=[0.22, 0.95, 0.8, 1.15])

Figure 4.1. Upward implementation of a graph. Nodes are implemented as objects and stored in an array. Edges are not implemented but only indicated by the function $A_{i,j}$, which takes a nonzero value if and only if $i$ and $j$ are connected by an edge.