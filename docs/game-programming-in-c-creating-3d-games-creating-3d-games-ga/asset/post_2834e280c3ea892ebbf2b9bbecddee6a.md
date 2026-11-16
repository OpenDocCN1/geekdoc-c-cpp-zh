
by power. However, a drawback of such a simple heuristic is that sometimes sacrificing a piece in the short term is better for the long term. Other heuristics might look at control of the board's center, the safety of the king, or the mobility of the queen. Ultimately, several different factors affect the heuristic.

More complex heuristics require more calculations. Most games institute some sort of time limit for AI moves. For example, a chess game AI might have only 10 seconds to decide its next move. This makes it necessary to strike a balance between the depth explored and heuristic complexity.

## Alpha-Beta Pruning

Alpha-beta pruning is an optimization of the minimax algorithm that, on average, reduces the number of nodes evaluated. In practice, this means it's possible to increase the maximum depth explored without increasing the computation time.

Figure 4.13 shows a game tree simplified by alpha-beta pruning. Assuming a left-to-right order of evaluation for siblings, the max player first inspects subtree B. The min player then sees the leaf with value 5, which means the min player has a choice between 5 and other values. If these other values are greater than 5, the min player obviously selects 5. This means that the upper bound of subtree B is 5, but the lower bound is negative infinity. The min player continues and sees the leaf with value 0 and selects this leaf because the min player wants the minimum possible score.

![](img/e9afcec1487716b0ef80d7e7c09869c8_292_0.png)

Figure 4.13 A game tree simplified by alpha-beta pruning

Control returns to the max player function, which now knows that subtree B has a value of 0. Next, the max player inspects subtree C. The min player first sees the leaf with value -3. As before, this means the upper bound of subtree C is -3. However, you already know that subtree B has a value of 0, which is better than -3. This means that there's no way subtree C can be better for the max player than subtree B. Alpha-beta pruning recognizes this and, as a result, does not inspect any other children of C.

Alpha-beta pruning adds two additional variables, called **alpha** and **beta**. **Alpha** is the best score guaranteed for the max player at the current level or higher. Conversely, **beta** is the best score guaranteed for the min player at the current level or higher. In other words, alpha and beta are the lower and upper bounds of the score.

Initially, alpha is negative infinity and beta is positive infinity—the worst possible values for both players. `AlphaBetaDecide`, in Listing 4.8, initializes alpha and beta to these values and then recurses by calling `AlphaBetaMin`.

### Listing 4.8 AlphaBetaDecide Implementation

Click here to view code image

```cpp
const GameState* AlphaBetaDecide(const GameState* root)
{
    const GameState* choice = nullptr;
    // Alpha starts at negative infinity, beta at positive infinity
    float maxValue = -std::numeric_limits<float>::infinity();
    float beta = std::numeric_limits<float>::infinity();
    for (const GameState* child : root->GetPossibleMoves())
    {
        float v = AlphaBetaMin(child, maxDepth - 1, maxValue, beta);
        if (v > maxValue)
        {
            maxValue = v;
            choice = child;
        }
    }
    return choice;
}
```

### Listing 4.9 AlphaBetaMax Implementation

Click here to view code image

```cpp
float AlphaBetaMax(const GameState* node, int depth,
                   float alpha, float beta)
{
    if (depth == 0 || node->IsTerminal())
    {
        return node->GetScore();
    }

    float maxValue = -std::numeric_limits<float>::infinity();
    for (const GameState* child : node->GetPossibleMoves())
    {
        maxValue = std::max(maxValue,
            AlphaBetaMin(child, depth - 1, alpha, beta));
        if (maxValue >= beta)
        {
            return maxValue; // Beta prune
        }

        alpha = std::max(maxValue, alpha); // Increase alpha
    }

    return maxValue;
}
```

### Listing 4.10 AlphaBetaMin Implementation

Click here to view code image

```cpp
float AlphaBetaMin(const GameState* node, int depth,
                   float alpha, float beta)
{
    if (depth == 0 || node->IsTerminal())
    {
        return node->GetScore();
    }

    float minValue = std::numeric_limits<float>::infinity();
    for (const GameState* child : node->GetPossibleMoves())
    {
        minValue = std::min(minValue,
                            AlphaBetaMax(child, depth - 1, alpha, beta));
        if (minValue <= alpha)
        {
            return minValue; // Alpha prune
        }
        beta = std::min(minValue, beta); // Decrease upper bound
    }

    return minValue;
}
```

Note that the order of evaluation for children affects the number of nodes pruned. This means that even with a consistent depth limit, different starting states yield different execution times. This can be problematic if the AI has a fixed time limit; an incomplete search means the AI has no idea which move to take. One solution is **iterative deepening**, which runs the algorithm multiple times at increasing depth limits. For example, first run alpha-beta pruning with a depth limit of three, which yields some baseline move. Then run with a depth limit of four, then five, and so on, until time runs out. At this point, the code returns the move from the previous iteration. This guarantees that some move is always available, even when time runs out.

## GAME PROJECT

This chapter's game project, shown in Figure 4.14, is a tower defense game. In this style of game, the enemies try to move from the start tile on the left to an end tile on the right. Initially, the enemies move in a straight line from left to right. However, the player can build towers on squares in the grid, even where the path is, which causes the path to redirect around these towers as needed. The code is available in the book's GitHub repository, in the `Chapter04` directory. Open Chapter04-windows.sln on Windows and Chapter04-mac.xcodeproj on Mac.

![](img/e9afcec1487716b0ef80d7e7c09869c8_298_0.png)

Figure 4.14 Chapter 4 game project

Use the mouse to click on and select tiles. After selecting a tile, use the B key to build a tower. The enemy airplanes path around the towers using the A* pathfinding algorithm. Each new tower built changes the path as necessary. To ensure that the player can't fully block in the enemies, when the player requests to build a tower, the code first ensures that a path would still exist for the enemies. If a tower would completely block the path, the game doesn't let the player build it.

As a simplification, the Tile class in the game project contains all the graph information, as well as the scratch data used by the A* search. The code that creates all the tiles and initializes the graph is in the constructor of the Grid class. The Grid class also contains the FindPath function that runs the actual A* search.

For completeness, the source code for this chapter also includes the versions of the search and minimax algorithms covered in the text in a separate Search.cpp file. It also includes the implementation of AIState and AIComponent, even though no actors in the game project use these features.

## SUMMARY

Artificial intelligence is a deep topic with many different sub-areas. Using state machines is an effective way to give behaviors to AI-controlled characters in a game. While a switch is the simplest implementation of a state machine, the state design pattern adds flexibility by making each state a separate class.

Pathfinding algorithms find the shortest path between two points in the game world. First, you formulate a graph representation for the game world. For a square grid, this is simple, but other games use path nodes or navigation meshes. For unweighted graphs, breadth-first search (BFS) guarantees to find the shortest path if one exists. But for weighted graphs, you need other algorithms, such as A* or Dijkstra's, to find the shortest path.
