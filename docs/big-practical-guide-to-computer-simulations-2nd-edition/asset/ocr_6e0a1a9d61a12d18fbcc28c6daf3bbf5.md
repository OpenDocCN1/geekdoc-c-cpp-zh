of starting arrays at index 0, we number the rows and columns from 0 to N − 1. Hence, initially the algorithm is called with n = N − 1.

We use an array pos[], where pos[c] stores the position of the queen in column c. If pos[c] = 0, no queen has been placed in that column. Hence, initially all pos[c] values are 0.

The array pos[] contains the complete information, hence it would suffice to use this array. Then, if one wants to test whether a queen in column c checks again any other queen, one has to run through the fields pos[c+1] to pos[N-1]. Hence, any such test would require O(N) operations. The test can be performed in O(1) steps, if additional arrays are used for all rows and all diagonals of the chess board, which indicate whether a queen is present or not in the row or diagonal. Hence, this is an example of how one can save running time at the expense of memory and by using more sophisticated data structures. This is a general balancing principle, which you should always keep in mind when designing your simulations.

![](bbox=[0.25, 0.55, 0.7, 0.75])

Fig. 6.5 “Up” and “down” diagonals {(c,r)} on the chessboard are characterized by c − r =const and c + r =const, respectively.

Coming back to the N-queens problem, note that diagonals come in two types. If we denote the coordinates by (c,r), “up diagonals” are characterized by c − r =const, while “down diagonals” are characterized by c + r =const, see Fig. 6.5. Here we use row, diag_up and diag_down, a value 0 always indicates that no queen is present, while a value 1 means that a queen has been placed. Note that there are 2N − 1 diagonals of each kind, hence these arrays must be larger (allocated in the main program, which is not shown here). Also note that for the up diagonals, c − r can be as small as −(N − 1), hence we shift the index of this array by this amount to start as usually at index 0. Using these additional arrays, the backtracking function for the queens problem

| GET SOURCE CODE |
| DIR: algorithms |
| FILE(S): queens.c |