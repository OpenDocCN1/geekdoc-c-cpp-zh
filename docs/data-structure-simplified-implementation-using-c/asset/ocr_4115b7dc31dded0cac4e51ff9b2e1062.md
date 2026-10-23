# F. Adjacency

In an undirected graph, if an edge ‘e’ is connected directly with the help of two vertices V_i, and V_j then both the edges are known as adjacent. Consider the graph illustrated in the figure 13.1, the edge ‘ab’ and ‘ac’ both are adjacent to ‘a’.

Table 13.1: Degree of graph in figure 13.2

| Vertex | In-degree | Out-degree | Degree |
|---|---|---|---|
| A | 0 | 2 | 2 |
| B | 2 | 2 | 4 |
| C | 1 | 2 | 3 |
| D | 2 | 0 | 2 |

# G. Path

Path in a graph is a set of vertices used to reach from the source to the destination. For instance, consider the graph of figure 13.2 the path between the sources ‘a’ to the destination ‘f’ is ‘ac-> ce-> ef’.

The graphs in which the path encompasses of all the vertices of a graph then it is known as Hamiltonian path.

# H. Cycle

In any graph, if we start from the source vertex and return to the vertex from where we have started(source vertex), then we term that the cycle is formed. In the directed graph, we may have a path from source to destination that may not form the cycle. However, in the undirected graph probability that the cycle is formed is increasingly higher, since, undirected graph does not involve the direction.

# I. Weighted graph

Graphs in which edges are assigned the weight, such kind of graphs are termed as weighted edges. Weighted graph is illustrated in the figure 13.4. In the illustrated figure, weight of the edges E12=7, and E13=5.

# 13.3 REPRESENTATION OF GRAPHS

Graphs that were created in the earlier sections are in the pictorial form. Same cannot be meaningful for the computer. We need to evolve the strategy in order to ensure that the graphs can be represented in the computer; this is known as representation of a graph. Following are the various methods which can be used to represent the graph.