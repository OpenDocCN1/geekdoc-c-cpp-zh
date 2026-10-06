# 180 CHAPTER 5 Recursion as a Problem-Solving Technique

FIGURE 5-8 A solution to the Eight Queens problem

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|--|
| ♜ | | | | | | | |
| | | | | | ♜ | | |
| | | ♜ | | | | | |
| | | | | ♜ | | | | |
| | | | | | | ♜ | |
| | | | | | | | ♜ | |
| | | | ♜ | | | | |

Figure 5-8 indicates the solution that the previous algorithm found. By modifying the arguments to placeQueens, you can discover other solutions to the Eight Queens problem. The Programming Problems at the end of this chapter ask you to consider other solutions to this algorithm, as well as additional modifications.

+   **Question 7** Consider a Four Queens problem, which has the same rules as the Eight Queens problem but uses a 4×4 board. Find all solutions to this new problem by applying backtracking by hand.

**Implementing eight queens using the STL class vector.** The Board class in the solution described thus far may be represented in a number of ways. The simplest representation would be a two-dimensional array; however, such array wastes space because only squares out of 64 are used. Another approach would be to use a one-dimensional array of only the squares that contain a queen. Because the algorithm uses backtracking, a dynamic array is the optimal choice. The vector container is often used in place of an array type, which allows the number of elements to vary dynamically and provides several built-in methods. Indexing is provided with array-type subscribing or with the at method, which provides range checking as well.

As in Listing 5-1, the class Board contains a vector of Queen objects, as well as several methods to manipulate the queens on the board. The class Queen appears in Listing 5-2.

# LISTING 5-1 The header file for the Board class

```
/** @file Board.h * */
#ifndef _BOARD
#define _BOARD
#include "Queen.h"
#include <vector>
#include <cassert>
```