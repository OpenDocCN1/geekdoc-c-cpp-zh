
![](img/723fa3ef35f5102eb67dc45b74bb823d_246_0.png)

| | V1 | V2 | V3 | V4 |
|---|---|---|---|---|
| V1 | 0 | 3 | 4 | 1 |
| V2 | 3 | 0 | 2 | 0 |
| V3 | 4 | 2 | 0 | 3 |
| V4 | 1 | 0 | 3 | 0 |

### Figure 9.15: Adjacency Matrix representation of undirected weighted graph

## Advantages of adjacency matrix

The adjacency matrix is very convenient to work with. Add or remove an edge can be done in O(1) time, the same time is required to check if there is an edge between two vertices. It is very easy to implement adjacency matrix of a graph.

## Disadvantages of adjacency matrix

- i) Adjacency matrix consumes a huge volume of memory for storing big graph. For dense graph adjacency matrix is optimal, but for a sparse graph where not much edges are connected this matrix is not essential.
- ii) The complexity of scanning an adjacency matrix during the implementation of graph searching algorithm like DFS is very high O(V2), which can be reduced to O(|V|+|E|).
- iii) To analyze a graph using adjacency matrix is time-consuming, as we need to go through all the rows and columns.

## Incident Matrix

Let G(V, E) be a graph with n vertices where n ≥ 1 and m edges where m ≥ 1. The incident matrix of G is the two-dimensional (n × m) array say A, with the property that A[i][j] = 1 if there is a relation between the edge ej and vertex vi in E(G). A[i][j] = 0, if there is no relationship between the edge ei and vertex vj. The relation between edge and vertex is known as “-incident” relation.

## Incident Matrix Representation for an Undirected Graph (G)

![](img/723fa3ef35f5102eb67dc45b74bb823d_246_1.png)

| | e1 | e2 | e3 | e4 | e5 |
|---|---|---|---|---|---|
| V1 | 1 | 0 | 1 | 1 | 0 |
| V2 | 1 | 1 | 0 | 0 | 0 |
| V3 | 0 | 1 | 1 | 0 | 1 |
| V4 | 0 | 0 | 0 | 1 | 1 |

### Figure 9.16: Incident Matrix representation of undirected graphs

## Incident Matrix Representation for a Directed Graph (G’)

For a directed graph, the relation between vertex and edge is represented in two ways. This is because in the case of directed graphs the edges are either outgoing edge that are coming out from a vertex or incoming edge that is the edge incident on the vertex. Depending on the relation, there are two types of incident matrix.

## Example:

![](img/723fa3ef35f5102eb67dc45b74bb823d_247_0.png)

| | e1 | e2 | e3 | e4 | e5 |
|---|---|---|---|---|---|
| V1 | 1 | 0 | 0 | 0 | 1 |
| V2 | 0 | 1 | 0 | 0 | 0 |
| V3 | 0 | 0 | 1 | 0 | 0 |
| V4 | 0 | 0 | 0 | 1 | 0 |

| | e1 | e2 | e3 | e4 | e5 |
|---|---|---|---|---|---|
| V1 | 0 | 0 | 1 | 0 | 0 |
| V2 | 1 | 0 | 0 | 0 | 0 |
| V3 | 0 | 1 | 0 | 1 | 0 |
| V4 | 0 | 0 | 0 | 0 | 1 |

(a) Out-degree

(b) In degree

### Figure 9.17: Incident Matrix representation of directed graphs (a) in degree & (b) out degree

## Advantages

It is easy to draw and analyze an undirected graph by the use of Incident graph.

## Disadvantages

- i) Require more memory space for storing a graph.
- ii) For a directed graph in degree and out degree, the matrix should be computed during implementation.
- iii) Time-consuming.

## Adjacency Lists

In this representation, the "n" rows of the adjacency matrix are represented as "n" linked list. There is one list for each vertex in G. The vertex in the list I represent the vertex that is adjacent to vertex i. Each vertex has at least two fields, one for vertex and another for the link with next vertex. The vertex field contains the index of the vertex adjacent to vertex i.

Structure definition of a vertex in Adjacency list is:

```
struct vertex
{
    int vertex;
    struct vertex *link;
};
```

## Adjacency list representation for an Undirected Graph (G)

In the case of the undirected graph with "n" vertices and "e" edges, this representation requires "n" head vertices and "2e" list vertices. The degree of any vertex in an undirected graph may be determined by just counting the number of vertices in the adjacency list. The total number of edges in graph G may be determined in time O(n+2e). If n << e then time complexity is O(2e) = O(e).

![](img/723fa3ef35f5102eb67dc45b74bb823d_248_0.png)

### Figure 9.18: Adjacency list representation for an Undirected Graph (G)

## Adjacency list representation for a Directed Graph (G’)

In the case of directed graph number of head vertices n and a number of list vertices e. The out-degree of a directed graph of any vertex may be determined by counting the number of vertices on its adjacency list. The total amount of time can, therefore, be determined in O(n + e). If n << e, then complexity is O(e).

![](img/723fa3ef35f5102eb67dc45b74bb823d_248_1.png)

### Figure 9.19: Adjacency list representation for a Directed Graph (G’)

## Inverse Adjacency list representation for a Directed Graph (G’)

To determine the in-degree of a vertex of a directed graph another list is considered which is termed as an inverse adjacency list of a directed graph.

![](img/723fa3ef35f5102eb67dc45b74bb823d_248_2.png)

### Figure 9.20: Inverse Adjacency list representation for a Directed Graph (G’)

## Advantages

The adjacency list allows us to store the graph in more compact form than adjacency matrix, but the difference decreases as a graph becomes denser. The next advantage is that the adjacency list allows getting the list of adjacent vertices in O(1) time, which is a big advantage for some algorithms.

## Disadvantages

- i) Adding/removing an edge to/from the adjacent list is not as easy as for adjacency matrix. It requires, on the average (|E| / |V|) time, which may result in cubic complexity for dense graphs to add all edges.
- ii) The adjacency list does not allow us to make an efficient implementation if a dynamic change of vertex number is required. Adding a new vertex can be done in O(V), but removal results in O(E) complexity.

## Orthogonal List

Alternatively, one could adopt a simplified version of the list structure called orthogonal list used for sparse matrix representation. Each vertex would now have four fields and would represent one edge.

The vertex structure would be:

```
struct vertex
{
    int head, tail;
    struct vertex *hp, *tp;
};
```

## Example:

![](img/723fa3ef35f5102eb67dc45b74bb823d_249_0.png)

### Figure 9.21: Orthogonal list representation for a Directed Graph (G)

## Adjacency Multi-lists

Adjacency multi-lists are an edge-based, rather than vertex-based, graph representation. In the adjacency list representation of an undirected graph, each edge (v1, v2) is represented by two entries. One on the list for v1, and the other on the list for v2. As it is observed in some situations, it is necessary to be able to determine the second entry for a particular edge and mark that edge as already having been examined. This can be accomplished easily if the adjacency lists are actually maintained as multi-lists.

For each edge, there will be exactly one vertex, but this vertex will be in two lists. The vertex structure is:

```
struct vertex
{
    int m;
    int v1, v2;
    struct vertex *p1, *p2;
};
```

| Mark(m) | 1st vertex(v1) | 2nd vertex(v2) | 1st path(p1) | 2nd path(p2) |
|---|---|---|---|---|

## Example:

![](img/723fa3ef35f5102eb67dc45b74bb823d_250_0.png)

- List of edges:
- Edge (1, 2) → N1
- Edge (1, 3) → N2
- Edge (1, 4) → N3
- Edge (2, 3) → N4
- Edge (2, 4) → N5
- Edge (3, 4) → N6

- List of vertices/paths:
- Vertex 1: N1 → N2 → N3
- Vertex 2: N1 → N4 → N5
- Vertex 3: N2 → N4 → N6
- Vertex 4: N3 → N5 → N6

![](img/723fa3ef35f5102eb67dc45b74bb823d_250_1.png)

### Figure 9.22: Adjacency Multi-list representation for a Directed Graph (G)

## Algorithm for Adjacency Matrix Creation for a Graph G

In the following algorithm, N represents a number of vertices and Adj[i][] is the adjacency matrix of the graph. Adj[i][j] is set to 1 if there is an edge between the vertices i and j else it is set to 0.

## Algorithm to create an adjacency matrix of a graph

```
Algorithm: CREATE (G)
[G is a given graph of N vertices]
```
