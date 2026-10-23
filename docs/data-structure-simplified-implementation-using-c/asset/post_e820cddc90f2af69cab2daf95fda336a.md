
# B. Directed Graph

In a graph, if we denote the direction in edges then it is termed as directed graph, it is illustrated in the figure 13.2. Such kind of graph is also known as ordered graph. In the directed graph of figure 13.2, the edge ‘ad’ is not same as ‘da’. We can distinguish the edges from one another with the help of the direction given.

Consider a case, if there is a need to visit from vertex ‘a’ to ‘f’. In this case, one path is ‘ac’, ‘ce’, ‘ef’ and the other possible path exist is ‘ab’, ‘bf’. Whereas, if we aim to reach ‘a’ from ‘f’

![](img/9b7c80a1312a664ae505ba138aa3306b_317_0.png)

Figure 13-1: Graph with vertices and edges

![](img/9b7c80a1312a664ae505ba138aa3306b_317_1.png)

Figure 13-2: Directed graph with six vertex

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

![](img/9b7c80a1312a664ae505ba138aa3306b_320_0.png)

# Figure 13-4: Weighted graph

### 13.3.1 Adjacency matrix

Adjacency matrix uses the matrix form to represent the edges between the two vertexes. If the vertex Vᵢ is connected to the Vertex Vⱼ with the help of a link known as edge then we represent this edge as ‘1’. In case, if it is not connected then it is represented as ‘0’. We have enumerated the adjacency matrix of the graph of figure 13.1 in the following table.

# Table 13.2: Adjacency matrix of the figure 13.1

|   | a | b | c | d | e | f | G | h |
|---|---|---|---|---|---|---|---|---|
| a | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| b | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| c | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 |
| d | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 |
| e | 0 | 0 | 1 | 0 | 1 | 1 | 1 | 0 |
| f | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
| g | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 |
| h | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

In the undirected graph, if the edge exists between the vertexes Aᵢ to the Vertex Aⱼ then 1 is to be placed in the edge Aᵢⱼ as well as the edge Aⱼᵢ, since direction does not have any significance in undirected graph. Adjacency matrix obtained for the undirected graph is symmetric that implies that if the edge exist from the vertex Aᵢ to Aⱼ then it also applies for the

Aᵢ to Aᵢ. Degree of any vertex can be determined with the help of adjacency matrix. **Degree of any node is the sum of all the 1 in a particular row of the vertex.** In table 13.2, we can determine the degree of vertex ‘c’ as 4. Correspondingly, degree of other vertex can be determined.

In the directed graph, adjacency matrix is significantly different from that of undirected graph. In case of directed graph, only those edges are considered that represent the edge between the two vertices of the graph. For instance, if we say ‘ab’ it means we assume that the edge will be directed from ‘a’ to ‘b’. if we consider ‘ba’ it is significantly different from the ‘ab’ where the direction is from source ‘a’ towards the destination ‘b’, whereas in the ‘ba’ edge is from the ‘b’ to the ‘a’.

**Table 13.3:** Adjacency matrix of figure13.2

|   | a | b | c | d | e | f | g |
|---|---:|---:|---:|---:|---:|---:|---:|
| a | 0 | 1 | 0 | 1 | 0 | 0 | 0 |
| b | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| c | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| d | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| e | 0 | 0 | 0 | 1 | 0 | 1 | 0 |
| f | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

In the directed graph, an edge may exist from the vertex Vᵢ to Vⱼ, however, that may not be true for the edge Vⱼ to Vᵢ. Therefore, adjacency matrix for the directed graph is not symmetric.

Degree of directed graph can be defined as sum of in-degree and out-degree of any vertex. In-degree of any directed graph is the total number of ‘1’ in that column, whereas out-degree in a directed graph is the total number of ‘1’ in the row. Consequently, degree of any node can be computed as:

*Degree of vertex (Vᵢ) = in-degree of vertex (Vᵢ) + out-degree of vertex (Vᵢ)*

### 13.3.2 Adjacency List

In the adjacency list, we create the link list for the vertex and all other nodes adjacent to it. For instance, each vertex represents the link list, nodes of this vertex is represented by the adjacent vertex. Therefore, all the nodes that are adjacent can be accessed from the particular node is taken into the single adjacency list. Adjacency list of figure 13.1 is illustrated in figure 13.5. Adjacency list can be created using the link list program. Similarly, adjacency list for the directed graph can be created like undirected graph. However, there is a minor difference that is attributed due to the involvement of directional component of the

directed graph. Adjacency list of the directed graph as illustrated in the figure 13.2 has been illustrated in the following figure 13.6

![](img/9b7c80a1312a664ae505ba138aa3306b_322_0.png)

Figure 13-6: Adjacency list of figure 13.1

![](img/9b7c80a1312a664ae505ba138aa3306b_322_1.png)

Figure 13-5: Adjacency list for the directed graph of figure 13.2

In the adjacency list, vertex ‘b’ and’d’ does not have any adjacency list consequently, they will point to the NULL.

### 13.3.3 Incidence matrix

Consider the graph ‘G’ with “n” vertices and “ne” edges but does not have any self-loop. Consider the matrix A= (a_ij) with n x ne, where n is the number of vertices and ne is the number of edges as follows.

A_ij=1 if “e_j” is incident to the vertex “v_i”
=0, otherwise

Such a matrix is known as the incidence matrix of a graph. In other terms incidence matrix

are the edges that are incident on a particular vertex. Therefore, we write all the incidence edges and all the vertex. If the incidence edge belongs to that particular vertex then 1 is placed otherwise 0. Consider the graph of the figure 13.7, In this graph, incidences are (1, 2), (2, 3), (2, 4) (3, 5) (3, 6) (3, 7). Incidence of figure 13.7 has been depicted in the following table 13.4.

Adjacency incidence matrix for the directed graph is different from the undirected graph. For any edge a_ij of a graph, incidence matrix is derived as per the following rule.

+   A_ij=1 if "e_i" is the incident out of V_i.
+   = -1 if "e_i" is the incident into V_i
+   = 0 if "ei" is not an incident to V_i.

![](img/9b7c80a1312a664ae505ba138aa3306b_323_0.png)

# Table 13.4: Incidence matrix for the figure 13.7

|  | (1,2), | (2,3) | (2,4) | (3,5) | (3,6) | (3,7) |
|---|---|---|---|---|---|---|
| 1. | 1 | 0 | 0 | 0 | 0 | 0 |
| 2. | 1 | 1 | 1 |  | 0 | 0 |
| 3. | 0 | 1 |  | 1 | 1 | 1 |
| 4. | 0 | 0 | 1 | 0 | 0 | 0 |
| 5. | 0 | 0 | 0 | 1 | 0 | 0 |
| 6. | 0 | 0 | 0 | 0 | 1 | 0 |
| 7. | 0 | 0 | 0 | 0 | 0 | 1 |
