
Here is a summary of the concepts we have introduced:

## Weighted Edges and Shortest Paths

A weighted edge is an edge together with a non-negative integer called the edge's weight.

The weight of a path is the total sum of the weights of all edges in the path. (Note: The weight of the empty path, with no edges, is always zero.)

If two vertices are connected by at least one path, then we can define the shortest path between two vertices. This is the path that has the smallest weight. (There may be several paths with equally small weights, in which case each of the paths is called "smallest.")

## Shortest-Distance Algorithm

In this section we will present an efficient algorithm called Dijkstra's algorithm (named for computer scientist Edsger Dijkstra, who proposed the algorithm) for finding the shortest path between two vertices. Throughout the section we will use graphs with weighted edges where each weight is a non-negative integer. We will use pseudocode rather than a particular language such as C++.

We start with a problem that's simpler than actually finding the shortest path from one vertex to another. We'll concentrate on simply finding the weight of the shortest path—in other words, the smallest possible sum of edge weights along a path from one vertex to another. This weight is called the shortest distance.

Dijkstra's algorithm actually provides more information than just the shortest distance from one vertex to another. In fact, the algorithm provides the shortest distance from a starting vertex (which we call start) to every vertex in the graph. The algorithm uses an integer array called distance, with one component for each vertex in the graph. Here is the algorithm's goal:

> we'll actually find shortest distances rather than shortest paths

## Goal of the Shortest-Distance Algorithm

The goal is to completely fill the distance array so that for each vertex v, the value of distance[v] is the weight of the shortest path from start to v.

We'll illustrate how the algorithm works with this small graph:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_793_0.png)

The algorithm begins by filling in one value in the distance array. We fill in 0 for the component that is indexed by the start vertex itself, indicating that the weight of the shortest path from the start vertex to the start vertex itself is zero. This is correct since the empty path exists from the start vertex to itself. At this point, the distance array has one known value:

| distance | 0 | ? | ? | ? | ? | ? |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

At this point we have one correct value, distance[0]. In the other locations we will write a value based on what we know so far. Because we don't know too much, our initial values won't be too accurate, but that's okay. In fact, the values that we fill in will all be infinity, represented by the symbol ∞. The distance array, with mostly ∞, is shown here:

| distance | 0 | ∞ | ∞ | ∞ | ∞ | ∞ |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

In an actual implementation, we would use some special integer value for ∞. For example, we could use -1 and make sure that all the rest of our programming always treats an occurrence of -1 as if it were infinity.

Now we are ready to do some processing that will steadily improve the values in the distance array. We begin with an observation about the initial values that we've placed in the distance array. These initial values are actually correct, if we are permitting only the empty path and ignoring all other paths. In other words, if the empty path is the only path that we are permitting, then there is a path from the start vertex to itself (namely the empty path with weight 0). But there is no way to get from the start vertex to any other vertex, and the fact that there is no path is represented by ∞ in the distance array.

Of course, permitting only the empty path is an overwhelming restriction. The key to the algorithm is in gradually relaxing this restriction, allowing more vertices to appear in permitted paths. As more and more vertices are allowed, we will continually revise the distance array so that its values are correct, for paths that pass through only allowed vertices. By the end of the algorithm, all vertices are allowed, and the distance array has values that are entirely correct.

the algorithm gradually improves the values in the distance array

The idea we have described needs some refinement. How are newly allowed vertices selected? How do we keep track of which vertices are currently allowed? How is the distance array revised at each step? These questions are addressed in the following list of three steps for the complete algorithm:

- Step 1. Fill in the distance array with ∞ at every location with the exception of distance[start], which is assigned the value zero.

- Step 2. Initialize a set of vertices, called allowed_vertices, to be the empty set. Throughout the algorithm a permitted path is a path that starts at the start vertex, and where each vertex on the path (except perhaps the final vertex) is in the set of allowed vertices. The final vertex on a permitted path does not need to be in the allowed_vertices set. At this point, allowed_vertices is the empty set, so the only permitted path is the empty path without any edges. (This empty path does contain one vertex, the start vertex. But since this vertex is the final vertex on the path, the vertex is not required to be in the allowed vertices set.)

- Step 3. The third step is a loop. Each time through the loop we will add one more vertex to allowed_vertices and then update the distance array so that all the allowed vertices may appear on paths. Here's a brief summary of the loop:

  ```
  // Loop in Step 3 of the shortest-distance algorithm:
  // n is the number of vertices in the graph
  for (allowed_size = 1; allowed_size <= n; ++allowed_size)
  {
    // At this point, allowed_vertices contains allowed_size - 1 vertices,
    // which are the allowed_size - 1 closest vertices to the start vertex.
    // Also, for each vertex v, distance[v] is the shortest distance from the
    // start vertex to vertex v, provided that we are considering only
    // permitted paths (i.e., paths where each vertex except the final
    // vertex must be in allowed_vertices).
  }
  ```

  - Step 3a. Let next be the closest vertex to the start vertex that is not yet in the set of allowed vertices (if several vertices are equally close, then you may choose next to be any of them).

  - Step 3b. Add the vertex next to the set allowed_vertices.

  - Step 3c. Revise the distance array so that the new vertex (next) may appear on permitted paths.

The loop's computation hinges on the condition written just before Step 3a. The condition indicates that the allowed_vertices set actually contains the allowed_size-1 vertices that are closest to the start vertex. The condition also indicates that distance[v] is always the shortest distance from the start vertex to vertex v, provided that we are considering only permitted paths (that is, paths where all vertices except the final vertex must be in the set of allowed vertices). This condition is true the first time the loop is entered, and it is also true at the start of each subsequent iteration. The responsibility of the three steps—3a, 3b, and 3c—is to ensure that the condition remains valid at the start of each iteration. Let’s examine the three steps in some detail.

Step 3a. This step must determine which of the unallowed vertices is closest to the start vertex. There is a simple rule for choosing this vertex:

> How to Choose the Next Vertex in Step 3a
> 
> In Step 3a, we will always choose the unallowed vertex that has the smallest current value in the distance array. (If several vertices have equally small distances, then we may choose any of them.)

For example, suppose we reach Step 3a, and we have this situation:

| distance | 0 | 2 | 10 | 17 | ∞ | 8 |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

In this example, the two shaded vertices, 0 and 1, are already in the set of allowed vertices.

Since vertices 0 and 1 are already in the allowed set, we may not choose them as the next vertex. Among the other vertices, vertex 5 has the smallest current value in the distance array (the value is 8). So we would choose vertex 5 as the next vertex. In the answer to Self-Test Exercise 21, we will explain precisely why this rule works, but for now it is sufficient to know that this is the correct way to select the next vertex.

Step 3b. In this step we “add the vertex next to the set allowed_vertices.” The implementation of this step depends on how the set of allowed vertices is represented. One possibility is to implement allowed_vertices as a set of vertex numbers, using set<int> from the Standard Template Library. In this case, Step 3b merely inserts next into the set.
