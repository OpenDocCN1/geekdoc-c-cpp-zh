# Chapter 3

# Algorithms 91

Find a source, output it, and delete it from the graph.

Repeat until the graph is empty.

Can you see why this generates a valid linearization for any day? What happens if the graph has cycles? And, how can this algorithm be implemented in linear time? (Exercise 3.14.)

# 3.4 Strongly connected components

# 3.4.1 Defining connectivity for directed graphs

Connectivity in undirected graphs is pretty straightforward: a graph that is not connected can be decomposed in a natural and obvious manner into several components (Figure 3.6 is a case in point). As we saw in Section 3.2.3, depth-first search does this happily, with each restart marking a new connected component.

In directed graphs, connectivity is more subtle. In some primitive sense, the directed graph of Figure 3.9(a) is “connected”—it can’t be “pulled apart,” so to speak, without breaking edges. But this notion —is hardly interesting or informative. The graph cannot be considered connected, because for instance there is no path from G to B or from F to A. The right way to define connectivity for directed graphs is this:

> Two nodes u and v of a directed graph are connected if there is a path from u to v and a path from v to u.

**Figure 3.9** (a) A directed graph and its strongly connected components. (b) The meta-graph.

![](bbox=[0.271, 0.621, 0.952, 0.866])