
### FIGURE 20-3 Graphs that are (a) connected; (b) disconnected; and (c) complete

![](img/288a0c22d14d2450c1e772f228f867b0_631_0.png)

Union, and finally back to the Library. Although a path may pass through the same vertex more than once, as the path just described does, a **simple path** may not. The path Dormitory–Library–Student Union is a simple path. A **cycle** is a path that begins and ends at the same vertex; a **simple cycle** is a cycle that does not pass through other vertices more than once. The path Library–Student Union–Gymnasium–Dormitory–Library is a simple cycle in the graph in Figure 20-2a. A graph is **connected** if each pair of distinct vertices has a path between them. That is, in a connected graph you can get from any vertex to any other vertex by following a path. Figure 20-3a shows a connected graph. Notice that a connected graph does not necessarily have an edge between every pair of vertices. Figure 20-3b shows a **disconnected** graph.

- A simple path passes through a vertex only once
- A cycle is a path that begins and ends at the same vertex
- A connected graph has a path between each pair of distinct vertices
- A complete graph has an edge between each pair of distinct vertices
- A complete graph is connected
- A multigraph has multiple edges and so is not a graph
- The edges of a weighted graph have numeric labels
- Each edge in a directed graph has a direction

In a **complete graph**, each pair of distinct vertices has an edge between them. The graph in Figure 20-3c is complete. Clearly, a complete graph is also connected, but the converse is not true; notice that the graph in Figure 20-3a is connected but is not complete.

Because a graph has a **set** of edges, a graph cannot have duplicate edges between vertices. However, a **multigraph**, as illustrated in Figure 20-4a, does allow multiple edges. Thus, a multigraph is not a graph. A graph’s edges cannot begin and end at the same vertex. Figure 20-4b shows such an edge, which is called a **self edge** or **loop**.

You can **label** the edges of a graph. When these labels represent numeric values, the graph is called a **weighted graph**. The graph in Figure 20-5a is a weighted graph whose edges are labeled with the distances between cities.

All of the previous graphs are examples of **undirected graphs**, because the edges do not indicate a direction. That is, you can travel in either direction along the edges between the vertices of an undirected graph. In contrast, each edge in a **directed graph**, or **digraph**, has a direction and is called a

### FIGURE 20-4 (a) A multigraph is not a graph; (b) a self edge is not allowed in a graph

![](img/288a0c22d14d2450c1e772f228f867b0_631_1.png)

### FIGURE 20-5 (a) A weighted graph; (b) a directed graph

![](img/288a0c22d14d2450c1e772f228f867b0_632_0.png)

> In a directed graph, vertex y is adjacent to vertex x if there is a directed edge from x to y

directed edge. Although each distinct pair of vertices in an undirected graph has only one edge between them, a directed graph can have two edges between a pair of vertices, one in each direction. For example, the airline flight map in Figure 20-5b is a directed graph. There are flights in both directions between Providence and New York, but although there is a flight from San Francisco to Albuquerque, there is no flight from Albuquerque to San Francisco. You can convert an undirected graph to a directed graph by replacing each edge with two directed edges that point in opposite directions. The definitions just given for undirected graphs apply also to directed graphs, with changes that account for direction. For example, a directed path is a sequence of directed edges between two vertices, such as the directed path in Figure 20-5b that begins in Providence, goes to New York, and ends in San Francisco. However, the definition of adjacent vertices is not quite as obvious for a digraph. If there is a directed edge from vertex x to vertex y, then y is adjacent to x. (Alternatively, y is a successor of x, and x is a predecessor of y.) It does not necessarily follow, however, that x is adjacent to y. Thus, in Figure 20-5b, Albuquerque is adjacent to San Francisco, but San Francisco is not adjacent to Albuquerque.

## 20.2 Graphs as ADTs

> Vertices can have values

You can treat graphs as abstract data types. Insertion and removal operations are somewhat different for graphs than for other ADTs that you have studied, in that they apply to either vertices or edges. You can define the ADT graph so that its vertices either do or do not contain values. A graph whose vertices do not contain values represents only the relationships among vertices. Such graphs are not unusual, because many problems have no need for vertex values. However, the following ADT graph operations do assume that the graph’s vertices contain values.

- **Note: ADT graph operations**
  - Test whether a graph is empty.
  - Get the number of vertices in a graph.
  - Get the number of edges in a graph.
  - See whether an edge exists between two given vertices.
  - Insert a vertex in a graph whose vertices have distinct values that differ from the new vertex’s value.
  - Insert an edge between two given vertices in a graph.
  - Remove a particular vertex from a graph and any edges between the vertex and other vertices.
  - Remove the edge between two given vertices in a graph.
  - Retrieve from a graph the vertex that contains a given value.

Several variations of this ADT are possible. For example, if the graph is directed, you can replace occurrences of “edges” in the previous operations with “directed edges.” You can also add traversal operations to the ADT. Graph-traversal algorithms are discussed in Section 20.3. Listing 20-1 contains an interface that specifies in more detail the ADT operations for an undirected graph.

### LISTING 20-1 A C++ interface for undirected, connected graphs

```
/* An interface for the ADT undirected, connected graph.
// File: GraphInterface.h
*/
#ifndef _GRAPH_INTERFACE
#define _GRAPH_INTERFACE
template<class LabelType>
class GraphInterface
{
public:
/** Gets the number of vertices in this graph.
@pre None.
@return The number of vertices in the graph. */
virtual int getNumVertices() const = 0;
/** Gets the number of edges in this graph.
@pre None.
@return The number of edges in the graph. */
virtual int getNumEdges() const = 0;
/** Creates an undirected edge in this graph between two vertices
that have the given labels. If such vertices do not exist, creates
them and adds them to the graph before creating the edge.
@param start A label for the first vertex.
@param end A label for the second vertex.
@param edgeWeight The integer weight of the edge.
@return True if the edge is created, or false otherwise. */
virtual bool add(LabelType start, LabelType end, int edgeWeight) = 0;
/** Removes an edge from this graph. If a vertex has no other edges,
it is removed from the graph since this is a connected graph.
@pre None.
@param start A label for the first vertex.
@param end A label for the second vertex.
@return True if the edge is removed, or false otherwise. */
virtual bool remove(LabelType start, LabelType end) = 0;
/** Gets the weight of an edge in this graph.
@return The weight of the specified edge.
If no such edge exists, returns a negative integer. */
virtual int getEdgeWeight(LabelType start, LabelType end) const = 0;
/** Performs a depth-first search of this graph beginning at the given
vertex and calls a given function once for each vertex visited.
@param start A label for the first vertex.
@param visit A client-defined function that performs an operation on
or with each visited vertex. */
virtual void depthFirstTraversal(LabelType start, void visit(LabelType&)) = 0;
/** Performs a breadth-first search of this graph beginning at the given
vertex and calls a given function once for each vertex visited.
@param start A label for the first vertex.
@param visit A client-defined function that performs an operation on
or with each visited vertex. */
virtual void breadthFirstTraversal(LabelType start, void visit(LabelType&)) = 0;
}; // end GraphInterface
#endif
```

### 20.2.1 Implementing Graphs

The two most common implementations of a graph are the adjacency matrix and the adjacency list. An adjacency matrix for a graph with n vertices numbered 0, 1, ... n - 1 is an n by n array matrix such that matrix[i][j] is 1 (true) if there is an edge from vertex i to vertex j, and 0 (false) otherwise. Figure 20-6 shows a directed graph and its adjacency matrix. Notice that the diagonal entries matrix[i][i] are 0, although sometimes it can be useful to set these entries to 1. You should choose the value that is most convenient for your application.

When the graph is weighted, you can let matrix[i][j] be the weight that labels the edge from vertex i to vertex j, instead of simply 1, and let matrix[i][j] equal infinity when there is no edge from vertex i to vertex j. For example, Figure 20-7 shows a weighted undirected graph and its adjacency matrix. Notice that the adjacency matrix for an undirected graph is symmetrical; that is, matrix[i][j] equals matrix[j][i].

Our definition of an adjacency matrix does not mention the value, if any, in a vertex. If you need to associate values with vertices, you can use a second array, values, to represent the n vertex values. The array values is one-dimensional, and values[i] is the value in vertex i.

An **adjacency list** for a graph with n vertices numbered 0, 1, ... n - 1 consists of n linked chains. The ith linked chain has a node for vertex j if and only if the graph contains an edge from vertex i to vertex j. This node can contain the vertex j's value, if any. If the vertex has no value, the node needs to contain some indication of the vertex's identity. Figure 20-8 shows a directed graph and its adjacency list. You can see, for example, that vertex 0 (P) has edges to vertex 2 (R) and vertex 5 (W). Thus, the first linked chain in the adjacency chain contains nodes for R and W.

Figure 20-9 shows an undirected graph and its adjacency list. The adjacency list for an undirected graph treats each edge as if it were two directed edges in opposite directions. Thus, the edge
