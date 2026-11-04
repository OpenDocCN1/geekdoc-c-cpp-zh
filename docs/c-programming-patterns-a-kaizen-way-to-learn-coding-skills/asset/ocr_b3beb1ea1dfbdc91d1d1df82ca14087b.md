# ExerciseYBE: Alphabet E

| | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2* | 1,3* | 1,4* | 1,5* |
| row=2 | 2,1 | 2,2 | 2,3 | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2 | 3,3 | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2 | 4,3 | 4,4 | 4,5 |
| row=5 | 5,1 | 5,2 | 5,3 | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2 | 6,3 | 6,4 | 6,5 |
| row=7 | 7,1* | 7,2* | 7,3* | 7,4* | 7,5* |

We need to put * characters in the first row and the last row.
So matching logical conditions will be (row==1) and (row==7).
Also by putting * characters in the second column will complete the alphabet E.
On adding logical condition (col==2), the total logical conditions becomes
(row==1)|| (row==7)|| (col==2)

| | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2* | 1,3* | 1,4* | 1,5* |
| row=2 | 2,1 | 2,2* | 2,3 | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2* | 3,3 | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2* | 4,3 | 4,4 | 4,5 |
| row=5 | 5,1 | 5,2* | 5,3 | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2* | 6,3 | 6,4 | 6,5 |
| row=7 | 7,1* | 7,2* | 7,3* | 7,4* | 7,5* |

Adding one more condition
(row==4 && col>=2) to the previous conditions.
The AND logical condition (&& col>=2) is because we don’t want to put * character in the box with value pair (4, 1).
The AND logical condition is applied to provide restriction in selecting data and our data are (row, col) value pairs, the boxes in general.

The total logical conditions becomes (row==1)|| (row==7)|| (col==2)|| (row ==4 && col>=2)

| | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2* | 1,3* | 1,4* | 1,5* |
| row=2 | 2,1 | 2,2* | 2,3 | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2* | 3,3 | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2* | 4,3* | 4,4* | 4,5 |
| row=5 | 5,1 | 5,2* | 5,3 | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2* | 6,3 | 6,4 | 6,5 |
| row=7 | 7,1* | 7,2* | 7,3* | 7,4* | 7,5* |

OR
*   *   *   *
    *
    *
    *   *   *
    *
    *
*   *   *   *