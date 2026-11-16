# 2.3 Artificial Intelligence Applications

![](bbox=[0.15, 0.08, 0.95, 0.34])

Figure 2.5 A possible state of knowledge is in (a) and a breadth-first tree that determines a shortest route to an unvisited, OK square based on that knowledge is in (b).

route to an unvisited OK square. The root (level 0) of the tree contains the agent's location. At level 1 of the tree we visit OK squares adjacent to the root. At level 2 of the tree we visit OK squares adjacent to level 1 squares, at level 3 we visit OK squares adjacent to level 2 squares, and so on. We only visit OK squares that are not already in the tree. We prune a node in the tree whenever there are no eligible squares adjacent to it. We continue until there are no nodes to expand (there is no possible safe route to an unvisited, OK square), or until we reach an unvisited, OK square. The node concerning square [1,1] at level 2 is pruned because the only OK square adjacent to it is square [2,1] which is already in the tree when square [1,1] is visited. The node concerning square [3,3] is also pruned because the only OK squares adjacent to it are already in the tree (by the time we investigate expanding that node). The shortest safe route to an unvisited, OK square is found to be one leading to square [1,4].

If there is no safe route to an unvisited, OK square, the agent's next course of action could be to plan a shortest safe route to a square which has a good chance of enabling the agent to kill the wumpus. If that is not possible, the agent could look for a shortest safe route to an unvisited square that is not known to not be OK. Finally, the agent could like for a shortest route to an unvisited square that is not known to be OK, which only goes through squares that are not known to not be OK. If this is not possible, the agent should give up as there is no way to reach the gold.

The algorithm follows.