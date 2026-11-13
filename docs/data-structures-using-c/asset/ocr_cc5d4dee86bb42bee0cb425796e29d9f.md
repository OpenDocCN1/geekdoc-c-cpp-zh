Let \( (V, E) \) be a graph and let \( e \in E \) be a directed edge associated with the ordered pair of nodes \( (a, b) \). Then, the edge \( e \) is said to be an initiating or originating in the node \( a \) and terminating or ending in the node \( b \). The nodes \( a \) and \( b \) are also called the initial and terminal nodes respectively, of the edge \( e \). An edge \( e \in E \) that joins the nodes \( a \) and \( b \), be it directed or undirected, is said to be incident to the nodes \( e \) and \( b \), respectively. An edge of a graph that joins a node to itself is called a loop (sling). Note that this loop is different from the loop in a program. The direction of the loop has no significance.

# Parallel Edges and Multigraph

![](bbox=[0.58, 0.26, 0.9, 0.43])

The graph given in Fig. 7.2(a) has only one edge between any pair of nodes. In the directed edges, the two possible edges between the pair of nodes that are opposite in direction are considered distinct. In some directed as well as undirected graphs, there may exist more than one edge incident to the same pair of nodes, say \( a \) and \( b \).

![](bbox=[0.58, 0.44, 0.9, 0.63])

In Fig. 7.2(b), the edges \( e_1, e_2 \), and \( e_3 \) are incident to vertices \( a \) and \( b \). Such edges are called as *parallel edges*. Here, \( e_1, e_2 \), and \( e_3 \) are three parallel edges. In addition, \( e_5 \) and \( e_6 \) are two parallel edges. Any graph that contains parallel edges is called a *multigraph*. On the other hand, a graph that has no parallel edges is called a *simple graph*.

Fig. 7.2 Classification based on edges (a) Simple graph (b) Multigraph

# Weighted Graph

A graph where weights are assigned to every edge is called a *weighted graph*. Weights can also be assigned to vertices. A graph of areas and streets of a city may be assigned weights according to its traffic density. A graph of areas and connecting roads may be assigned weights such that the distance between the cities is assigned to edges and area population is assigned to vertices.

# Null Graph and Isolated Vertex

In a graph, a node that is not adjacent to any other node is called an *isolated node*. A graph containing only isolated nodes is called a *null graph*. Hence, the set of edges is an empty set in a null graph.

Let \( V = \) set of students, \( E = \) (there exists an edge incident to two students if they share books). Let \( V = \{a, b, c\} \). If no two students among \( a, b \), and \( c \) share books, then the graph \( G = \{V, E\} \) is represented as shown in Fig. 7.3(a).