# Figure 8.3 What is the smallest cut in this graph?

![](bbox=[0.433, 0.116, 0.768, 0.283])

budget $b$, to find a cut with at most $b$ edges. For example, the smallest cut in Figure 8.3 is of size 3. This problem can be solved in polynomial time by $n-1$ max-flow computations: give each edge a capacity of 1, and find the maximum flow between some fixed node and every single other node. The smallest such flow will correspond (via the max-flow min-cut theorem) to the smallest cut. Can you see why? We've seen a very different, randomized algorithm for this problem (page 140).

In many graphs, such as the one in Figure 8.3, the smallest cut joins a singleton vertex on one side—it consists of all edges adjacent to this vertex. Far more interesting are small cuts that partition the vertices of the graph into nearly equal sets. More precisely, the BALANCED CUT problem is this: given a graph with $n$ vertices and a budget $b$, partition the vertices into two sets $S$ and $T$ such that $|S|, |T| \geq n/3$ and that there are at most $b$ edges between $S$ and $T$. Other hard problem

Balanced cuts arise in a variety of important applications, such as clustering. Consider the problem of segmenting an image into its constituent components (say, an elephant standing in a grassy plain with a clear blue sky). A good way of doing this is to create a graph with a node for each pixel of the image and to put an edge between nodes whose pixels are spatially close together and are also similar in color. A single object in the image (like the elephant) then corresponds to a set of highly connected vertices in the graph. A balanced cut is therefore likely to divide the pixels into two clusters without breaking any of the primary constituents of the image. The first cut, for instance, separate the elephant on one hand from the sky and grass from the other. A further cut would then be needed to separate the sky from the grass.

# Integer linear programming

Even though the simplex algorithm is not polynomial time, we mentioned in Chapter 7 that there is a different, polynomial algorithm for linear programming. Therefore, linear programming is efficiently solvable both in practice and in theory. The situation changes completely if, in addition to specifying a linear objective function