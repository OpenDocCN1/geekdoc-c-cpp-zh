# Click here to view code image

```
NodeToParentMap map;

bool found = BFS(g, g.mNodes[0], g.mNodes[9], map);
```

If BFS succeeds, you can reconstruct the path by using the parent pointers in the *outMap*. This is because the goal's parent points to the preceding node on the path. Similarly, the parent of the node preceding the goal node is two moves away from the goal. Following this chain of parent pointers eventually leads back to the start node, yielding a path from goal to start.

Unfortunately, you want the path in the opposite direction: from start to goal. One solution is to reverse the path with a stack, but a more intelligent approach is to *reverse the search*. For example, instead of passing in the mouse node as start and the cheese node as goal, do the opposite. Then, following the parent pointers from the goal node yields the desired path.

BFS always finds a path between the start and goal nodes if one exists. But for weighted graphs, BFS doesn't guarantee to find the shortest path. This is because BFS doesn't look at the weight of the edges at all; every edge traversal is equivalent. In *Figure 4.6*, the dashed path has the shortest distance, but BFS returns the solid path as it requires only two moves.