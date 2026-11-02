![](bbox=[0.04, 0.14, 0.92, 0.48])

Fig. 6.30 (left) The 8 possible moves of a knight. (right) A possible solution of the knight's tour problem for a 8 × 8 chessboard.

Design, implement and test the resulting program. Hints: Use an array visit[x][y], where initially visit[x][y]=0 everywhere, and where visit[x][y]>0 indicates at which stage of the tour the square is visited. Furthermore, use arrays dx[] and dy[] which store the possible move, e.g. (see left of Fig. 6.30) dx[0]=−2 and dy[0]=−1. Finally, you could use a function, which places exactly one knight and calls itself for placing the next knight. The function prototype could look as follows:

```
/********************* move_knight() *********************/
/** Calculates recursively via backtracking a tour for **/
/** the knight, such that all squares with visit[x][y]=0 **/
/** are visited once. **/
/** **/
/** Parameters: (*) = return parameter **/
/** n: size of board **/
/** step: how many sites already visited? **/
/** x,y: current position of knight **/
/** visit: states whether and when square was visited **/
/** dx,dy: possible move directions **/
/** Returns: **/
/** (nothing) **/
/********************************************************** */
void move_knight(int n, int step, int x, int y,
 short int **visit, int *dx, int *dy)
```

# (5) Remove element from list

Design, implement and test the function remove_node() for removing elements from a list, as described on page 181. The function prototype reads as follows:

SOLUTION SOURCE CODE
DIR: algorithms
FILE(S): list_rm_e.c