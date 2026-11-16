distance equation is as follows:

```
h (x) \sqrt{(start.x - end.x)^2 + (start.y - end.y)^2}
```

The Euclidean distance function is almost always admissible, even in cases where the Manhattan distance is inadmissible. This means that Euclidean distance is usually the recommended heuristic function. However, the Manhattan heuristic is more efficient to compute because it doesn’t involve a square root.

The only case where a Euclidean distance heuristic overestimates the true cost is if the game allows non-Euclidean movement such as teleporting between two nodes across the level.

Notice that in Figure 4.7 both heuristic h(x) functions end up underestimating the actual cost of traveling from the start node to the goal node. This happens because the heuristic function knows nothing about the adjacency lists, so it doesn’t know whether certain areas are impassable. This is fine because the heuristic is the lower bound of how close node x is to the goal node; the heuristic guarantees that node x is at least that distance away. This is more useful in a relative sense: The heuristic can help estimate whether node A or node B is closer to the goal node. And then you can use this estimate to help decide whether to explore node A or node B next.

The following section shows how to use the heuristic function to create a more complex pathfinding