
Step 3c. Finally, we must revise the distance array so that the newly allowed vertex, next, is permitted on a path from the start vertex to another vertex. An example will explain the necessary revisions. Suppose that vertices 0, 1, and 5 are already in the allowed_vertices set, and that we have just added vertex 2 as our next vertex, as shown here:

| 0 | 2 | 10 | 17 | 11 | 8 |
|---|---|---|---|---|---|
| [0] | [1] | (2) | [3] | [4] | [5] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_796_0.png)

The shaded vertices are the vertices that were already allowed, and we have just added vertex 2 as the next allowed vertex.

Since we have just added vertex 2 as a newly allowed vertex, we must now update the distance array to reflect the fact that vertex 2 may now appear on paths.

For example, distance[3] is currently 17. This means that there is a path from the start vertex to vertex 3 that uses only vertices 0, 1, and 5, and that has a length of 17. Here's the key question: if we also allow vertex 2 to appear on a path from the start vertex to vertex 3, can we obtain a distance that is smaller than 17? A smaller distance might be possible by taking a two-part path, shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_796_1.png)

The first part of the path goes from the start vertex v0 to the newly allowed vertex v2 ...

... and the second part of the path consists of one more edges from the newly allowed vertex v2 to vertex v3.

This path has two parts: the part from the start vertex to vertex 2, followed by the part that has the single edge from vertex 2 to vertex 3. The total weight of this path is:

```
distance[2] + (weight of the edge from vertex 2 to vertex 3)
```

In our example, this sum is 11, which is smaller than the current “best distance to vertex 3.” Therefore we should replace distance[3] with this smaller sum. We must also create similar two-part paths for each of the other unallowed vertices, and if the two-part path is smaller than the current distance, then we modify the distance array. This provides the following refined pseudocode for Step 3c:

## Step 3c. Revise the distance array so that the new vertex (next) may appear on permitted paths. The integer n is the number of vertices; v and sum are local integer variables, as shown in this code:

```
for (v = 0; v < n; ++v)
    if ((v is not an allowed vertex) and (there is an edge from next to v))
    {
        sum = distance[next] + (weight of the edge from next to v);
        if (sum < distance[v])
            distance[v] = sum;
    }
```

Notice that we do not consider a possible new smaller distance to vertices that are already allowed vertices. That is because these vertices are all closer to the start vertex than next is, so that distance[next] is going to be larger than the shortest distance to any of these vertices.

Also, when we are creating the new two-part paths, we consider only the case where the second part of the path is a single edge from next to the end vertex. The reason for this is that a longer path from next to the end vertex would have to pass through other allowed vertices, meaning that we have a path that goes from the start vertex, through next, through another allowed vertex, and finally to the end vertex. But such a path will always be shorter by avoiding the next vertex altogether—just go from the start vertex to that other allowed vertex (using the shortest path) and then to the end vertex. Such a path, which does not go through the next vertex, is already permitted. We don’t need to consider such a path again—we need to consider only new paths that pass through the next newly allowed vertex.

The complete pseudocode for the algorithm is shown in Figure 15.4. The main loop actually stops at the number of vertices minus 1 because at that point there is only one unallowed vertex, and this must be the farthest vertex from the start vertex so that no shortest paths can go through this farthest vertex.

We'll execute the algorithm on our example graph. Here's the situation after initializing the distance array:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_798_0.png)

| | 0 | ∞ | ∞ | ∞ | ∞ | ∞ |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

At this point, the set of allowed vertices is empty, and we will enter the main loop for the first time. In Step 3a, the value of next is set to vertex 0 (since distance[0] is the smallest value in the distance array). We then look at each unallowed vertex v with an edge from vertex 0 to vertex v. These are vertices 1 and 5, so we check to see whether we need to revise distance[1] and distance[5]:

- distance[0] + (the weight of the edge from 0 to 1) is 2. Since this is smaller than the current value of distance[1], we replace distance[1] with 2.
- distance[0] + (the weight of the edge from 0 to 5) is 9. Since this is smaller than the current value of distance[5], we replace distance[5] with 9.

At this point, the distance array is as shown here (with the allowed vertices shaded):

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_798_1.png)

| | 0 | 2 | ∞ | ∞ | ∞ | 9 |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

The currently allowed vertices are shaded.

## FIGURE 15.4 Dijkstra's Shortest-Distance Algorithm

### Pseudocode

**Input.** A directed graph with positive integer edge weights and n vertices. One of the vertices, called start, is specified as the start vertex.

**Output.** A list of the shortest distances from the start vertex to every other vertex in the graph.

The algorithm uses an array of n integers (called distance) and a set of vertices (called allowed_vertices). The variables v, allowed_size, and sum are local integer variables. There is some special value (\(\infty\)) that we can place in the distance array to indicate an infinite distance (which means there is no path).

- **Step 1.** Initialize the distance array to contain all \(\infty\), except distance[start], which is set to 0.

- **Step 2.** Initialize the set of allowed vertices to be the empty set.

- **Step 3.** Compute the complete distance array:

```
for (allowed_size = 1; allowed_size < n; ++allowed_size)
{
   // At this point, allowed_vertices contains allowed_size - 1 vertices, which are the
   // allowed_size - 1 closest vertices to the start vertex. Also, for each vertex v, distance[v]
   // is the shortest distance from the start vertex to vertex v, provided that we are
   // considering only permitted paths (i.e., paths where each vertex except the final vertex
   // must be in allowed_vertices).
}
```

- **Step 3a.** Let next be the closest vertex to the start vertex, which is not yet in the set of allowed vertices (if several vertices are equally close, then you may choose next to be any of them).

- **Step 3b.** Add the vertex next to the set allowed_vertices.

- **Step 3c.** Revise the distance array so that the new vertex (next) may appear on permitted paths:

```
for (v = 0; v < n; ++v)
   if ((v is not an allowed vertex) and (there is an edge from next to v))
   {
      sum = distance[next] + (weight of the edge from next to v);
      if (sum < distance[v])
         distance[v] = sum;
   }
```

- **Step 4.** Output the values in the distance array. (Each distance[v] is the shortest distance from the start vertex to vertex v.)

The second time we enter the main loop, the value of next is set to vertex 1 (since distance[1] is the smallest value of the unallowed vertices). We then look at each unallowed vertex v with an edge from vertex 1 to vertex v. These are vertices 2, 3, and 5, so we check to see whether we need to revise distance[2], distance[3], and distance[5]:

- distance[1] + (the weight of the edge from 1 to 2) is 10. Since this is smaller than the current value of distance[2], we replace distance[2] with 10.
- distance[1] + (the weight of the edge from 1 to 3) is 17. Since this is smaller than the current value of distance[3], we replace distance[3] with 17.
- distance[1] + (the weight of the edge from 1 to 5) is 8. Since this is smaller than the current value of distance[5], we replace distance[5] with 8.

At this point, the distance array is:

| | 0 | 2 | 10 | 17 | ∞ | 8 |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_800_0.png)

The currently allowed vertices are shaded.

The third time we enter the main loop, the value of next will be set to vertex 5 (since distance[5] is the smallest value of the unallowed vertices). We then look at each unallowed vertex v with an edge from vertex 5 to vertex v. Vertex 4 is the only vertex that is the target of an edge from vertex 5, so we check to see whether we need to revise distance[4]:

- distance[5] + (the weight of the edge from 5 to 4) is 11. Since this is smaller than the current value of distance[4], we replace distance[4] with 11.
