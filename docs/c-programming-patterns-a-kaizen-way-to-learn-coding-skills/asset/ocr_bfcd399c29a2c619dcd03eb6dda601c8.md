So it has two repetition process one for printing spaces and second for printing numeric values.

It means require 2 inner for-loops and 1 outer loop for iterating rows. The relation between row value and upper limit for inner-for-loop for spaces and numbers.

| Row level Repetitive Action | | | | | Expected Output |
|---|---|---|---|---|---|
| row | Column level Repetitive Action | | | | |
| | lower_limit<=col_sp<=upper_limit | | lower_limit<=col_num<=upper_limit | | |
| | lower_limit | upper_limit | lower_limit | upper_limit | |
| 5 | 1 | 0 | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 1 | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 2 | 1 | 3 | 3 3 3 |
| 2 | 1 | 3 | 1 | 2 | 2 2 |
| 1 | 1 | 4 | 1 | 1 | 1 |

The lower_limit for spaces & num variable has the same numeric value expression for all the rows.

It's consistent for all the rows. Likewise we need to come out with such a consistent expression for upper_limit for which it should suit any number of rows.

The other remaining variables are row & totalRows=5. Let's try to generalise using these variables.

| Column level Repetitive Action | | | | | | |
|---|---|---|---|---|---|---|
| row | lower_limit<=col_sp<=upper_limit | | | lower_limit<=col_num<=upper_limit | | Expected Output |
| | lower_limit | upper_limit | default | upper_limit | lower_limit | |
| 5 | 1 | 0 | totalRows - row | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 1 | totalRows - row | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 2 | totalRows - row | 1 | 3 | 3 3 3 |
| 2 | 1 | 3 | totalRows - row | 1 | 2 | 2 2 |
| 1 | 1 | 4 | totalRows - row | 1 | 1 | 1 |

Now the uppler_limit of col_sp variable related inner for-loop is generalised, same expression on all the rows. The lower_limit of col_num variable related inner for-loop is not generalised as not having same expression on all the rows.

Since lower_limit of col_num variable values matches with row variable values.