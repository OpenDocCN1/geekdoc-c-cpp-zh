
The analysis of the algorithm involves two factors. Suppose lines 9 to 11 and 18 to 20 are never executed. We can maintain D as a balanced binary search (or splay) tree (this would require a code modification, of course). If we never backtrack, there are at most O(N^2) operations involving D, such as deletion and the contents implied at lines 4, 12, and 13. This claim is obvious for deletions, since D has O(N^2) elements and no element is ever reinserted. Each call to place uses at most 2N contains, and since place never backtracks in this analysis, there can be at most 2N^2 contains. Thus, if there is no backtracking, the running time is O(N^2 log N).

Of course, backtracking happens, and if it happens repeatedly, then the performance of the algorithm is affected. This can be forced to happen by construction of a pathological case. Experiments have shown that if the points have integer coordinates distributed uniformly and randomly from [0, Dmax], where Dmax = \Theta(N^2), then, almost certainly, at most one backtrack is performed during the entire algorithm.

## 10.5.2 Games

As our last application, we will consider the strategy that a computer might use to play a strategic game, such as checkers or chess. We will use, as an example, the much simpler game of tic-tac-toe, because it makes the points easier to illustrate.

Tic-tac-toe is a draw if both sides play optimally. By performing a careful case-by-case analysis, it is not a difficult matter to construct an algorithm that never loses and always wins when presented the opportunity. This can be done, because certain positions are known traps and can be handled by a lookup table. Other strategies, such as taking the center square when it is available, make the analysis simpler. If this is done, then by using a table we can always choose a move based only on the current position. Of course, this strategy requires the programmer, and not the computer, to do most of theValue;
  int dc; // dc means don't care; its value is unused
  int value;

  if( fullBoard( ) )
    value = DRAW;
  else
    if( immediateCompWin( bestMove ) )
      return COMP_WIN; // bestMove will be set by immediateCompWin
    else
    {
      value = COMP_LOSS; bestMove = 1;
      for( i = 1; i <= 9; i++ ) // Try each square
      {
        if( isEmpty( i ) )
        {
          place( i, COMP );
          responseValue = findHumanMove( dc );
          unplace( i ); // Restore board
        }
        if( responseValue > value )
        {
          // Update best move
          value = responseValue;
          bestMove = i;
        }
      }
    }
  }
  return value;
}
```

Figure 10.67 Minimax tic-tac-toe algorithm: computer selection

positions, line 21 initializes it to the smallest possible value, and the loop in lines 22 to 37 searches for improvements. Each successor position is recursively evaluated in turn by Lines 26 to 28. This is recursive, because, as we will see, findHumanMove calls findCompMove. If the human's response to a move leaves the computer with a more favorable position than that obtained with the previously best computer move, then the value and bestMove are updated. Figure 10.68 shows the function for the human's move selection. The logic is virtually identical, except that the human player chooses the move that leads to the lowest-valued position. Indeed, it is not difficult to combine these two procedures into one by

```
int TicTacToe::findHumanMove( int & bestMove )
{
   int i, responseValue;
   int dc; // dc means don't care; its value is unused
   int value;

   if( fullBoard( ) )
      value = DRAW;
   else
      if( immediateHumanWin( bestMove ) )
         return COMP_LOSS;
      else
      {
         value = COMP_WIN; bestMove = 1;
         for( i = 1; i <= 9; ++i ) // Try each square
         {
            if( isEmpty( i ) )
            {
               place( i, HUMAN );
               responseValue = findCompMove( dc );
               unplace( i ); // Restore board
               if( responseValue < value )
               {
                  // Update best move
                  value = responseValue;
                  bestMove = i;
               }
            }
         }
      }
   return value;
}
```

Figure 10.68 Minimax tic-tac-toe algorithm: human selection

passing an extra variable, which indicates whose turn it is to move. This does make the code somewhat less readable, so we have stayed with separate routines.

We leave supporting routines as an exercise. The most costly computation is the case where the computer is asked to pick the opening move. Since at this stage the game is a forced draw, the computer selects square 1. A total of 97,162 positions were examined, and the calculation took a few seconds. No attempt was made to optimize the code. When the computer moves second, the number of positions examined is 5,185 if the human selects the center square, 9,761 when a corner square is selected, and 13,233 when a noncorner edge square is selected.

For more complex games, such as checkers and chess, it is obviously infeasible to search all the way to the terminal nodes.9 In this case, we have to stop the search after a certain depth of recursion is reached. The nodes where the recursion is stopped become terminal nodes. These terminal nodes are evaluated with a function that estimates the value of the position. For instance, in a chess program, the evaluation function measures such variables as the relative amount and strength of pieces and positional factors. The evaluation function is crucial for success, because the computer's move selection is based on maximizing this function. The best computer chess programs have surprisingly sophisticated evaluation functions.

Nevertheless, for computer chess, the single most important factor seems to be number of moves look-ahead the program is capable of. This is sometimes known as ply; it is equal to the depth of the recursion. To implement this, an extra parameter is given to the search routines.

The basic method to increase the look-ahead factor in game programs is to come up with methods that evaluate fewer nodes without losing any information. One method which we have already seen is to use a table to keep track of all positions that have been evaluated. For instance, in the course of searching for the first move, the program will examine the positions of Figure 10.69. If the values of the positions are saved, the second occurrence of a position need not be recomputed; it essentially becomes a terminal position. The data structure that records this is known as a transposition table; it is almost always implemented by hashing. In many cases, this can save considerable computation. For instance, in a chess endgame, where there are relatively few pieces, the time savings can allow a search to go several levels deeper.

### α-β Pruning

Probably the most significant improvement one can obtain in general is known as α-β pruning. Figure 10.70 shows the trace of the recursive calls used to evaluate some hypothetical position in a hypothetical game. This is commonly referred to as a game tree. (We have avoided the use of this term until now, because it is somewhat misleading: no

3 We numbered the squares starting from the top left and moving right. However, this is only important for the supporting routines.

4 It is estimated that if this search were conducted for chess, at least 10^100 positions would be examined for the first move. Even if the improvements described later in this section were incorporated, this number could not be reduced to a practical level.
