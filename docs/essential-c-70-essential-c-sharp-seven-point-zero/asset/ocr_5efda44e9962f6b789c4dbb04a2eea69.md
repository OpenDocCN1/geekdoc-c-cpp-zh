Initializing a tic-tac-toe board with a specific position could be done as shown in Listing 3.14.

# LISTING 3.14: Initializing a Two-Dimensional Array of Integers

```
`int[,] cells = {  {1, 0, 2},  {1, 2, 0},  {1, 2, 1} };`
```

The initialization follows the pattern in which there is an array of three elements of type `int[]`, and each element has the same size; in this example, the size is 3. Note that the sizes of each `int[]` element must all be identical. The declaration shown in Listing 3.15, therefore, is not valid.

# LISTING 3.15: A Multidimensional Array with Inconsistent Size, Causing an Error

```
`// ERROR: Each dimension must be consistently sized  int[,] cells = {  {1, 0, 2, 0},  {1, 2, 0},  {1, 2}  {1} };`
```

Representing tic-tac-toe does not require an integer in each position. One alternative is to construct a separate virtual board for each player, with each board containing a `bool` that indicates which positions the players selected. Listing 3.16 corresponds to a three-dimensional board.

# LISTING 3.16: Initializing a Three-Dimensional Array

```
```
bool[,] cells;
cells = new bool[2,3,3]
{
        // Player 1 moves                 // X |   |
        { {true, false, false},          //  -------
          {true, false, false},          // X |   |
          {true, false, true} },         //  -------
                                   // X |   | X

        // Player 2 moves                 //   |   | O
        { {false, false, true},          //  -----
          {false, true, false},          //   | O |
          {false, true, false} }         //  -----
                                   //   | O |
};
```
```