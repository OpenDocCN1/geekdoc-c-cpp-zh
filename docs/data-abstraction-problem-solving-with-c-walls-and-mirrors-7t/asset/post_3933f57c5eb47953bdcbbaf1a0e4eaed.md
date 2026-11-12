
### FIGURE 20-26 Checking weight[u] by examining the graph: (a) weight[2] in step 2; (b) weight[1] in step 3; (c) weight[3] in step 3; (d) weight[3] in step 4

![](img/288a0c22d14d2450c1e772f228f867b0_652_0.png)

include vertex 4 in the path. However, for vertex 2 notice that weight[2] = ∞ > weight[4] + matrix[4][2] = 4 + 1 = 5. Therefore, replace weight[2] with 5. You can also verify this conclusion by examining the graph directly, as Figure 20-26a shows.

**Step 3.** weight[2] = 5 is the smallest value in weight, ignoring weight[0] and weight[4] because 0 and 4 are in vertexSet. Thus, v = 2, so add 2 to vertexSet. For vertices not in vertexSet—that is, for u = 1 and 3—check whether it is shorter to go from 0 to 2 and then along an edge to u instead of directly from 0 to u along an edge. (See Figures 20-26b and 20-26c.)

Notice that

weight[1] = 8 > weight[2] + matrix[2][1] = 5 + 2 = 7. Therefore, replace weight[1] with 7.
weight[3] = 9 > weight[2] + matrix[2][3] = 5 + 3 = 8. Therefore, replace weight[3] with 8.

**Step 4.** weight[1] = 7 is the smallest value in weight, ignoring weight[0], weight[2], and weight[4] because 0, 2, and 4 are in vertexSet. Thus, v = 1, so add 1 to vertexSet. For vertex 3, which is the only vertex not in vertexSet, notice that weight[3] = 8 < weight[1] + matrix[1][3] = 7 + ∞, as Figure 20-26d shows. Therefore, leave weight[3] as it is.

**Step 5.** The only remaining vertex not in vertexSet is 3, so add it to vertexSet and stop.

The final values in weight are the weights of the shortest paths. These values appear in the last line of Figure 20-25. For example, the shortest path from vertex 0 to vertex 1 has a cost of weight[1], which is 7. This result agrees with our earlier observation about Figure 20-24. We saw then that the shortest path is from 0 to 4 to 2 to 1. Also, the shortest path from vertex 0 to vertex 2 has a cost of weight[2], which is 5. This path is from 0 to 4 to 2.

The weights in weight are the smallest possible, as long as the algorithm's loop invariant is true. The proof that the loop invariant is true is by induction on step, and is left as a difficult exercise. (See Exercise 20.)

## 20.4.5 Circuits

A circuit is simply another name for a type of cycle that is common in the statement of certain problems. Recall that a cycle in a graph is a path that begins and ends at the same vertex. Typical circuits either visit every vertex once or visit every edge once.

Probably the first application of graphs occurred in the early 1700s when Euler proposed a bridge problem. Two islands in a river are joined to each other and to the river banks by several bridges, as Figure 20-27a illustrates. The bridges correspond to the edges in the multigraph in Figure 20-27b, and the land masses correspond to the vertices. The problem asked whether you can begin at a vertex v, pass through every edge exactly once, and terminate at v. Euler demonstrated that no solution exists for this particular configuration of edges and vertices.

For simplicity, we will consider an undirected graph rather than a multigraph. A path in an undirected graph that begins at a vertex v, passes through every edge in the graph exactly once, and terminates at v is called an Euler circuit. Euler showed that an Euler circuit exists if and only if each vertex touches an even number of edges. Intuitively, if you arrive at a vertex along one edge, you must be able to leave the vertex along another edge. If you cannot, you will not be able to reach all of the vertices.

> An Euler circuit begins at a vertex v, passes through every edge exactly once, and terminates at v

### FIGURE 20-27 (a) Euler's bridge problem and (b) its multigraph representation

![](img/288a0c22d14d2450c1e772f228f867b0_653_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_653_1.png)

### FIGURE 20-28 Pencil and paper drawings

![](img/288a0c22d14d2450c1e772f228f867b0_654_0.png)

![](img/288a0c22d14d2450c1e772f228f867b0_654_1.png)

### FIGURE 20-29 Connected undirected graphs based on the drawings in Figure 20-28

![](img/288a0c22d14d2450c1e772f228f867b0_654_2.png)

![](img/288a0c22d14d2450c1e772f228f867b0_654_3.png)

Finding an Euler circuit is like drawing each of the diagrams in Figure 20-28 without lifting your pen or redrawing a line, and ending at your starting point. No solution is possible for Figure 20-28a, but you should be able to find one easily for Figure 20-28b. Figure 20-29 contains undirected graphs based on Figure 20-28. In Figure 20-29a, vertices h and i each touch an odd number of edges (three), so no Euler circuit is possible. On the other hand, each vertex in Figure 20-29b touches an even number of edges, making an Euler circuit feasible. Notice also that the graphs are connected. If a graph is not connected, a path through all of the vertices would not be possible.

Let's find an Euler circuit for the graph in Figure 20-29b, starting arbitrarily at vertex a. The strategy uses a depth-first search that marks edges instead of vertices as they are traversed. Recall that a depth-first search traverses a path from a as deeply into the graph as possible. By marking edges instead of vertices, you will return to the starting vertex; that is, you will find a cycle. In this example, the cycle is a, b, e, d, a if we visit the vertices in alphabetical order, as Figure 20-30a shows. Clearly this is not the desired circuit, because we have not visited every edge. We are not finished, however.

To continue, find the first vertex along the cycle a, b, e, d, a that touches an unvisited edge. In our example, the desired vertex is e. Apply our modified depth-first search, beginning with this vertex. The resulting cycle is e, f, j, i, e. Next you join this cycle with the one you found previously. That is, when you reach e in the first cycle, you travel along the second cycle before continuing in the first cycle. The resulting path is a, b, e, f, j, i, e, d, a, as Figure 20-30b shows.

The first vertex along our combined cycle that touches an unvisited edge is i. Beginning at i, our algorithm determines the cycle i, h, d, c, g, h, l, i. Joining this to our combined cycle results in the Euler circuit a, b, e, f, j, i, h, d, c, g, h, l, i, e, d, a. (See Figure 20-30c.)

### FIGURE 20-30 The steps to determine an Euler circuit for the graph in Figure 20-29b

![](img/288a0c22d14d2450c1e772f228f867b0_655_0.png)

## 20.4.6 Some Difficult Problems

The next three applications of graphs have solutions that are beyond the scope of this book.

The traveling salesperson problem. A Hamilton circuit is a path that begins at a vertex v, passes through every vertex in the graph exactly once, and terminates at v. Determining whether an arbitrary graph contains a Hamilton circuit can be difficult. A well-known variation of this problem—the traveling salesperson problem—involves a weighted graph that represents a road map. Each edge has an associated cost, such as the mileage between cities or the time required to drive from one city to the next. The salesperson must begin at an origin city, visit every other city exactly once, and return to the origin city. However, the circuit traveled must be the least expensive.

> A Hamilton circuit begins at a vertex v, passes through every vertex exactly once, and terminates at v

### FIGURE 20-31 The three utilities problem

![](img/288a0c22d14d2450c1e772f228f867b0_656_0.png)

Unfortunately for this traveler, solving the problem is no easy task. Although a solution does exist, it is quite slow, and no better solution is known.

The three utilities problem. Imagine three houses A, B, and C and three utilities X, Y, and Z (such as telephone, water, and electricity), as Figure 20-31 illustrates. If the houses and the utilities are vertices in a graph, is it possible to connect each house to each utility with edges that do not cross one another? The answer to this question is no.

A planar graph can be drawn so that no two edges cross

A graph is planar if you can draw it in a plane in at least one way so that no two edges cross. The generalization of the three utilities problem determines whether a given graph is planar. Making this determination has many important applications. For example, a graph can represent an electronic circuit where the vertices represent components and the edges represent the connections between components. Is it possible to design the circuit so that the connections do not cross? The solutions to these problems are also beyond the scope of this book.

The four-color problem. Given a planar graph, you can color the vertices so that no adjacent vertices have the same color, if you use at most four colors? For example, the graph in Figure 20-11 is planar because none of its edges cross. You can solve the coloring problem for this graph by using only three colors. Color vertices a, c, g, and h red, color vertices b, d, f, and j blue, and color vertex e green.

The answer to our question is yes, but it is difficult to prove. In fact, this problem was posed more than a century before it was solved in the 1970s with the use of a computer.

- Question 1 Describe the graph in Figure 20-32. For example, are they directed? Connected? Complete? Weighted?
- Question 2 Use the depth-first strategy and the breadth-first strategy to traverse the graph in Figure 20-32a, beginning with vertex 0. List the vertices in the order in which each traversal visits them.
- Question 3 Write the adjacency matrix for the graph in Figure 20-32a.
- Question 4 Add an edge to the directed graph in Figure 20-14 that runs from vertex d to vertex b. Write all possible topological orders for the vertices in this new graph.
- Question 5 Is it possible for a connected undirected graph with five vertices and four edges to contain a simple cycle? Explain.
