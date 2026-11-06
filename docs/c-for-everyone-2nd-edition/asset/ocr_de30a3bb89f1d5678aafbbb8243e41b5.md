generating random values until you have a value that is not yet in the array. But that is inefficient. Instead, follow this algorithm:

+   - Make a second array and fill it with the numbers 1 to 10.
+   - Repeat 10 times
+     - Pick a random element from the second array.
+     - Remove it and append it to the permutation array.

**P6.17** It is a well-researched fact that men in a restroom generally prefer to maximize their distance from already occupied stalls, by occupying the middle of the longest sequence of unoccupied places.

For example, consider the situation where all ten stalls are empty.

- - - - - - - - - -

The first visitor will occupy a middle position:

- - - - X - - - - -

The next visitor will be in the middle of the empty area at the right.

- - - - X - - X - -

Given an array of bool values, where true indicates an occupied stall, find the position for the next visitor. Your computation should be placed in a function

```
next_visitor(bool occupied[], int stalls)
```

**P6.18** In this assignment, you will model the game of *Bulgarian Solitaire*. The game starts with 45 cards. (They need not be playing cards. Unmarked index cards work just as well.) Randomly divide them into some number of piles of random size. For example, you might start with piles of size 20, 5, 1, 9, and 10. In each round, you take one card from each pile, forming a new pile with these cards. For example, the sample starting configuration would be transformed into piles of size 19, 4, 8, 9, and 5. The solitaire is over when the piles have size 1, 2, 3, 4, 5, 6, 7, 8, and 9, in some order. (It can be shown that you always end up with such a configuration.)

In your program, produce a random starting configuration and print it. Then keep applying the solitaire step and print the result. Stop when the solitaire final configuration is reached.

**P6.19** *Magic squares.* An n × n matrix that is filled with the numbers 1, 2, 3, . . . , n² is a magic square if the sum of the elements in each row, in each column, and in the two diagonals is the same value.

| 16 | 3 | 2 | 13 |
|---|---|---|---|
| 5 | 10 | 11 | 8 |
| 9 | 6 | 7 | 12 |
| 4 | 15 | 14 | 1 |

Write a program that reads in 16 values from the keyboard and tests whether they form a magic square when put into a 4 × 4 array. You need to test two features:

+   1. Does each of the numbers 1, 2, ..., 16 occur in the user input?
+   2. When the numbers are put into a square, are the sums of the rows, columns, and diagonals equal to each other?

**P6.20** Implement the following algorithm to construct magic n × n squares; it works only if n is odd.