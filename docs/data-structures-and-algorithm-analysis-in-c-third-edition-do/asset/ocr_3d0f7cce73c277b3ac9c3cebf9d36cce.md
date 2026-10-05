412

Chap. 11 Graphs

11.2 An undirected graph need not explicitly store two separate directed edges to represent a single undirected edge. An alternative would be to store only a single undirected edge (I, J) to connect Vertices I and J. However, what if the user asks for edge (J, I)? We can solve this problem by storing the edge such that the label of I and J always comes first. Thus, if we have an edge connecting Vertices 5 and 3, requests for edge (5, 3) and (3, 5) both map to (3, 5) because 3 < 5.

Looking at the adjacency matrix, notice that only the lower triangle of the array is used. We could cut the space by the adjacency matrix from |V|² positions to V(|V|-1)/2 positions. Read Section 12.2 on triangular matrices. The re-implement adjacency matrix representation of Figure 11.6 to implement undirected graphs using a triangular array.

11.3 While the undirected implementation (whether adjacency matrix or adjacency list) is hidden behind the graph ADT, these two implementations can have an impact on the efficiency of the resulting program. For Dijkstra's shortest path algorithm, two different implementations were given in Section 11.4.1 that provide different ways for determining the next vertex at each iteration of the algorithm. The relative costs of these two variants depend on whether sparse or dense graphs. They may also depend on whether the graph is implemented using an adjacency list or adjacency matrix.

Design and implement a study to compare the effects on performance for three variables: (i) the two graph representations (adjacency list and adjacency matrix); (ii) the two implementations for Dijkstra's shortest path algorithm (searching the table of vertex distances or using a priority queue to track the distances); and (iii) sparse versus dense graphs. Be sure to test your implementations on a variety of graphs that are sufficiently large to generate meaningful times.

11.4 The example implementations for DFS and BFS show calls to PreVisit and PostVisit. Re-implement the BFS and DFS functions to make use of the design pattern to handle the pre/post visit functionality.

11.5 Write a program to link the connected components for an undirected graph. In other words, all vertices of the first component are given the first component's label, all vertices of the second component are given the second component's label, and so on. Your algorithm should work by defining any two vertices connected by an edge to be members of the same equivalence class. Once all of the edges have been processed, all vertices in a given equivalence class will be connected. Use the UNION/FIND implementation from Section 6.2 to implement equivalence classes.