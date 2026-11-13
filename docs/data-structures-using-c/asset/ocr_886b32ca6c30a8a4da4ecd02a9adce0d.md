# RECAPITULATION

+   - Graphs are one of the most important non-linear data structures. A graph is a representation of relation. Vertices represent elements and edges represent relationships. In other words, a graph is a collection of nodes (vertices) and arcs joining pairs of the nodes (edges). The edges between two vertices represent the relationship between them.
+   - Graphs are classified as directed and undirected graphs. In an undirected graph, an edge is a set of two vertices where order does not make any relevance, whereas in a directed graph, an edge is an ordered pair.
+   - Graphs are implemented using an array or a linked list representation. An adjacency list is a data structure for representing a graph by keeping a list of the neighbour vertices for each vertex. An adjacency matrix is a data structure for representing a graph as a Boolean matrix where 0 means no edge and 1 corresponds to an edge.
+   - There are two standard graph traversals—depth-first and breadth-first.
+   - A minimum spanning tree is a tree, containing all the vertices of a graph, where the total weight of the edges is minimum. The two popularly used algorithms to compute minimum spanning tree are Prim's and Kruskal's algorithms.
+   - A biconnected component is a maximal sub-graph. A component of biconnected graph is useful in modelling a robust communication network.
+   - A disjoint set is a type of data structure that keeps track of a set of elements partitioned into a number of disjoint subsets. Operations such as union and find are performed on it for respectively merging two sets into one and determining the location of a given set.
+   - Dijkstra's algorithm is another common algorithm for graphs to find the shortest path between two vertices of a graph.

# KEY TERMS

+   - **Adjacency list** In an adjacency list, the n rows of the adjacency list are represented as n-linked lists, one list per vertex of the graph. We can represent G by an array Head, where Head[i] is a pointer to the adjacency list of vertex i. Each node of the list has at least two fields: vertex and link. The vertex field contains the vertex id, and link field stores the pointer to the next node storing another vertex adjacent to i.
+   - **Adjacency matrix** The graphs represented using a sequential representation using matrices is called an adjacency matrix.
+   - **Adjacency multilist** Multilists are lists where nodes may be shared among several other lists. For each edge, instead of two, there will be exactly one node, but this node will be in two lists, that is, the adjacency lists for each of the two nodes it is incident on.
+   - **Biconnected component** A biconnected component is a maximal biconnected sub-graph of graph G = (V, E) containing no separation vertices or edges.
+   - **Breadth-first search (BFS)** In BFS, all the unvisited vertices adjacent to i are visited after visiting the start vertex i and marking it visited. Next, the unvisited vertices adjacent to these vertices are visited and so on until the entire graph has been traversed.
+   - **Connected component** An undirected graph is connected if there is at least one path between