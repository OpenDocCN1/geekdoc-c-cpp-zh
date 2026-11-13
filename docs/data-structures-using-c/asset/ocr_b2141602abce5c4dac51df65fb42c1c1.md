means to maintain and manipulate data in many applications. Consider the following example:

![](bbox=[0.585, 0.105, 0.895, 0.335])

Fig. 7.1 Folder and subfolders organization

The operating system of a computer system organizes files into directories and sub-directories. Directories are also referred to as folders. The operating system organizes folders and files using a tree structure as in Fig. 7.1.

A folder contains other folders (subfolders) and files. This can be viewed as the tree drawn in Fig. 7.1. Note that the root here is desktop. The common uses of trees include the following:

+   1. Manipulating hierarchical data
+   2. Making information easily searchable
+   3. Manipulating sorted lists of data

A tree is a graph called the directed acyclic graph. So let us first discuss the basic terminology related to trees.

# ## 7.1.1 Basic Terminology

We should first learn about a general graph because trees can be viewed as restricted graphs. A graph G consists of a non-empty set V, a set E, and a mapping from the set E to set V. Here, V is the set of nodes, also called as vertices points, of the graph, and E is the set of edges of the graph. For finite graphs, V and E are finite. We can represent them as G = (V, E).

# ### Adjacent Nodes

If an edge e ∈ E is associated with a pair of nodes (a, b) where a, b ∈ V, then it is said that the edge e joins or connects the nodes a and b. Any two nodes that are connected with an edge are called as adjacent nodes.

# ### Directed and Undirected Graphs

In a graph G(V, E), an edge that is directed from one node to another is called a directed edge, whereas an edge that has the no specific direction is called an undirected edge. A graph where every edge is directed is called a directed graph or digraph. A graph where every edge is undirected is called as an undirected graph. If some of edges are directed and some are undirected in a graph, the graph is called as a mixed graph. A city map showing only the one-way streets is an example of a directed graph where the intersections are vertices and the edges are streets. A map showing only the two-way streets is an example of an undirected graph, and a map showing all the one-way and two-way streets is an example of a mixed graph.