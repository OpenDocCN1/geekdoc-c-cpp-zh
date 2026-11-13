# *Is_empty*

The is_empty operation checks whether the graph is empty and returns true if empty else returns false. An empty graph is one where the set V is a null set.

These are the basic operations on graphs, and a few more include getting the set of adjacent nodes of a vertex or an edge and traversing a graph. Checking the adjacency between vertices means verifying the relationship between them, and the relationship is maintained using a suitable data structure.

Graph traversal is also known as searching through a graph. It means systematically passing through the edges and visiting the vertices of the graph. A graph search algorithm can help in listing all vertices, checking connectivity, and discovering the structure of a graph. We shall discuss traversals in Section 8.4.

# 8.3 REPRESENTATION OF GRAPHS

We need to store two sets V and E to represent a graph. Here V is a set of vertices and E is a set of incident edges. These two sets basically represent the vertices and adjacency relationship among them. There are two standard representations of a graph given as follows:

+   1. Adjacency matrix (sequential representation) and
+   2. Adjacency list (linked representation)

Using these two representations, graphs can be realized using the adjacency matrix, adjacency list, or adjacency multilist. Let us study each of them.

# 8.3.1 Adjacency Matrix

Adjacency matrix is a square, two-dimensional array with one row and one column for each vertex in the graph. An entry in row i and column j is 1 if there is an edge incident between vertex i and vertex j, and is 0 otherwise. If a graph is a weighted graph, then the entry 1 is replaced with the weight. It is one of the most common and simple representations of the edges of a graph; programs can access this information very efficiently.

For a graph G = (V, E), suppose V = {1, 2, ..., n}. The adjacency matrix for G is a two-dimensional l x n Boolean matrix A and can be represented as
A[i][j] = { 1 if there exists an edge <i, j>
          0 if edge <i, j> does not exist }

The adjacency matrix A has a natural implementation as in the following: A[i][j] is 1 (or true) if and only if vertex i is adjacent to vertex j. If the graph is undirected, then
A[i][j] = A[j][i] = 1

If the graph is directed, we interpret 1 stored at A[i][j], indicating that the edge from i to j exists and not indicating whether or not the edge from j to i exists in the graph.

The graphs G1, G2, and G3 of Fig. 8.5 are represented using the adjacency matrix in Fig. 8.6, among which G2 is a directed graph.