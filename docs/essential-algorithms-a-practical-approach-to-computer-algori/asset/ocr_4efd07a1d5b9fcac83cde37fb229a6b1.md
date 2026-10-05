# Appendix B ■ Solutions to Exercises 531

+   - The game ended in a tie 46,080 times.
- The total number of possible games X was 255,168.

The numbers would favor player X if each player moved randomly, but because mostbeginners have a strategy that forces a tie, a tie is the most common outcome.

+   2. Example program CountPrefilledBoards does this. Figure-20 shows the number of possible games for each initial square taken. For example, 27,732 possible games start with X taking the upper-left corner on the first move.

| 27,732 | 29,592 | 27,732 |
| 29,592 | 25,872 | 29,592 |
| 27,732 | 29,592 | 27,732 |

**Figure B-20:** These numbers show how many possible games begin with X taking the corresponding square in the first move.

The tic-tac-toe board is symmetric, you don't really need to count the games from each starting position. All corners give the same number of possible games, and all the middle squares also give the same number of possible games. You only need to count the games for one corner, one middle, and the center to get all the values.

+   3. Example program TicTacToe does this.

+   4. Example program PartitionProblem does this.

+   5. Example program PartitionProblem does this.

+   6. Figure B-21 shows two graphs. The graph of the nodes visited is almost a perfectly straight line for both algorithms, so the number of nodes visited by each algorithm is an exponential function of the number of weights N. In other words, if N the number of weights, <NodesVisited> = C^N for some C. The number of nodes visited is smaller for branch and bound, but it's still exponential.

+   7. Example program PartitionProblem does this.

+   8. Example program PartitionProblem does this.

+   9. The two groups are [9, 6, 7, 7, 6] and [7, 7, 7, 5, 5]. Their total weights are 35 and 31, so the difference is 4.

+   10. Example program PartitionProblem does this.