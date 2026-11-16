by power. However, a drawback of such a simple heuristic is that sometimes sacrificing a piece in the short term is better for the long term. Other heuristics might look at control of the board's center, the safety of the king, or the mobility of the queen. Ultimately, several different factors affect the heuristic.

More complex heuristics require more calculations. Most games institute some sort of time limit for AI moves. For example, a chess game AI might have only 10 seconds to decide its next move. This makes it necessary to strike a balance between the depth explored and heuristic complexity.

# Alpha-Beta Pruning

Alpha-beta pruning is an optimization of the minimax algorithm that, on average, reduces the number of nodes evaluated. In practice, this means it's possible to increase the maximum depth explored without increasing the computation time.

Figure 4.13 shows a game tree simplified by alpha-beta pruning. Assuming a left-to-right order of evaluation for siblings, the max player first inspects subtree B. The min player then sees the leaf with value 5, which means the min player has a choice between 5 and other values. If these other values are greater than 5, the min player obviously selects 5. This means that the upper bound of subtree B is 5, but the lower bound is negative infinity. The min player continues and sees the leaf with value o and selects this leaf because the min player wants the