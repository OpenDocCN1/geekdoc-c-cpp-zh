# FIGURE 20-3 Graphs that are (a) connected; (b) disconnected; and (c) complete

![](bbox=[0.06, 0.13, 0.78, 0.29])

Union, and finally back to the Library. Although a path may pass through the same vertex more than once, as the path just described does, a simple path may not. The path Dormitory–Library–Student Union is a simple path. A cycle is a path that begins and ends at the same vertex; a simple cycle is a cycle that does not pass through other vertices more than once. The path Library–Student Union–Gymnasium–Dormitory–Library is a simple cycle in the graph in Figure 20-2a. A graph is connected if each pair of distinct vertices has a path between them. That is, in a connected graph you can get from any vertex to any other vertex by following a path. Figure 20-3a shows a connected graph. Notice that a connected graph does not necessarily have an edge between every pair of vertices. Figure 20-3b shows a disconnected graph.

In a complete graph, each pair of distinct vertices has an edge between them. The graph in Figure 20-3c is complete. Clearly, a complete graph is also connected, but the converse is not true; notice that the graph in Figure 20-3a is connected but is not complete.

Because a graph has a set of edges, a graph cannot have duplicate edges between vertices. However, a multigraph, as illustrated in Figure 20-4a, does allow multiple edges. Thus, a multigraph is not a graph. A graph’s edges cannot begin and end at the same vertex. Figure 20-4b shows such an edge, which is called a self edge or loop.

You can label the edges of a graph. When these labels represent numeric values, the graph is called a weighted graph. The graph in Figure 20-5a is a weighted graph whose edges are labeled with the distances between cities.

All of the previous graphs are examples of undirected graphs, because the edges do not indicate a direction. That is, you can travel in either direction along the edges between the vertices of an undirected graph. In contrast, each edge in a directed graph, or digraph, has a direction and is called a

+   - A simple path passes through a vertex only once
+   - A cycle is a path that begins and ends at the same vertex
+   - A connected graph has a path between each pair of distinct vertices
+   - A complete graph has an edge between each pair of distinct vertices
+   - A complete graph is connected
+   - A multigraph has multiple edges and so is not a graph
+   - The edges of a weighted graph have numeric labels
+   - Each edge in a directed graph has a direction

# FIGURE 20-4 (a) A multigraph is not a graph; (b) a self edge is not allowed in a graph

![](bbox=[0.06, 0.76, 0.78, 0.91])