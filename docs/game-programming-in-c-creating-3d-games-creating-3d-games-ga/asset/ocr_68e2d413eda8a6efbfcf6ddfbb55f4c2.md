```
// (A WeightedGraph has WeightedGraphNodes)
```

By referencing both the “from” and “to” nodes in each edge, you can support a directed edge from node A to B by adding an edge to node A’s mEdges vector but not to node B’s. If you want an undirected edge, you simply add two directed edges, one in each direction (for example, from A to B and from B to A).

Different games represent the game world via graphs in different manners. Partitioning a world into a grid of squares (or hexes) is the simplest approach. This approach is very popular for turn-based strategy games such as Civilization or XCOM. However, for many other types of games, it isn’t feasible to use this approach. For simplicity, most of this section sticks with a grid of squares. However, you will learn about other possible representations later in this chapter.

# Breadth-First Search

Suppose a game takes place in a maze designed in a square grid. The game only allows movement in the four cardinal directions. Because each move in the maze is uniform in length, an unweighted graph can represent this maze. Figure 4-5 shows a sample maze and its corresponding graph.