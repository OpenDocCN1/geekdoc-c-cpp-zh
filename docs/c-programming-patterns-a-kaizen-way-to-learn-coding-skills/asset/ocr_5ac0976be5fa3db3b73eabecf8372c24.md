# COLUMN LEVEL REPETITIVE ACTION

| Row level Repetitive Action | Expected Output |
|---|---|
| row | Column level Repetitive Action | |
|  | lower_limit <=col<= upper_limit | upper_limit >=num >= lower_limit | |
|  | lower_limit | upper_limit | upper_limit | lower_limit | |
| 5 | 1 | 0 | 9 | 5 | 9 8 7 6 5 |
| 4 | 1 | 1 | 7 | 4 | 7 6 5 4 |
| 3 | 1 | 2 | 5 | 3 | 5 4 3 |
| 2 | 1 | 3 | 3 | 2 | 3 2 |
| 1 | 1 | 4 | 1 | 1 | 1 |

The lower_limit for spaces & num variable has the same numeric value expression for all the rows.

It's consistent for all the rows. Likewise we need to come out with such a consistent expression for upper_limit for which it should suit any number of rows.

The other remaining variables are row & totalRows=5. Let's try to generalise using these variables.

| Column level Repetitive Action | |
| row | lower_limit <=spaces<= upper_limit | upper_limit >=num >= lower_limit |
|  | lower_limit | upper_limit | upper_limit | lower_limit |
|  |  | default | 1 | default | 1 |
| 5 | 1 | 0 | totalRows - row | 9 | 5 | row |
| 4 | 1 | 1 | totalRows - row | 7 | 4 | row |
| 3 | 1 | 2 | totalRows - row | 5 | 3 | row |
| 2 | 1 | 3 | totalRows - row | 3 | 2 | row |
| 1 | 1 | 4 | totalRows - row | 1 | 1 | row |

The upper_limit of row variable related inner for-loop is generalised, consistent expression on all the rows.

The upper_limit of num variable related inner for-loop is not generalised as not having expression on all the rows. From previous cases we know it can follow the generalised expression 2*row - 1.

| Column level Repetitive Action | |
| row | lower_limit <=spaces<= upper_limit | upper_limit >=num >= lower_limit |
|  | lower_limit | upper_limit | upper_limit | lower_limit |
|  |  | default | 1 | 2*row - 1 | 1 |
| 5 | 1 | 0 | totalRows - row | 2*row - 1 | row |
| 4 | 1 | 1 | totalRows - row | 2*row - 1 | row |
| 3 | 1 | 2 | totalRows - row | 2*row - 1 | row |
| 2 | 1 | 3 | totalRows - row | 2*row - 1 | row |
| 1 | 1 | 4 | totalRows - row | 2*row - 1 | row |

So the upper_limit of col & num variables are generalised.

The lower_limit & upper_limit are consistent for all the rows. It's now generalised for any number of rows.

So it has two repetition process one for printing spaces and second for printing numeric values.

It means require 2 inner for-loops and 1 outer loop for iterating rows.