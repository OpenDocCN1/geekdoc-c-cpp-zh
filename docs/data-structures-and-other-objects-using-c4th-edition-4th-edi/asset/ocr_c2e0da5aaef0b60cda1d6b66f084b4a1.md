In our example, this sum is 11, which is smaller than the current “best distance to vertex 3.” Therefore we should replace distance[3] with this smaller sum. We must also create similar two-part paths for each of the other unallowed vertices, and if the two-part path is smaller than the current distance, then we modify the distance array. This provides the following refined pseudocode for Step 3c:

# Step 3c. Revise the distance array so that the new vertex (next) may appear on permitted paths. The integer n is the number of vertices; v and sum are local integer variables, as shown in this code:

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