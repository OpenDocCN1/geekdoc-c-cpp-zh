# ExerciseYBD: Alphabet D

We need to put * characters in the first row and the last row. So matching logical conditions will be (row==1) and (row==7).

![](bbox=[0.1, 0.25, 0.35, 0.55])

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2* | 1,3* | 1,4* | 1,5* |
| row=2 | 2,1 | 2,2 | 2,3 | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2 | 3,3 | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2 | 4,3 | 4,4 | 4,5 |
| row=5 | 5,1 | 5,2 | 5,3 | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2 | 6,3 | 6,4 | 6,5 |
| row=7 | 7,1* | 7,2* | 7,3* | 7,4* | 7,5* |

Now by putting * characters in the second column and the last column will complete the alphabet D. The logical conditions columns will be (col==2) and (col==5).Total logical conditions becomes (row==1) || (row==7) || (col==2) || (col==5)

Removing all the (row, col) value pair that doesn't have * characters.

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2* | 1,3* | 1,4* | 1,5* |
| row=2 | 2,1 | 2,2* | 2,3 | 2,4 | 2,5* |
| row=3 | 3,1 | 3,2* | 3,3 | 3,4 | 3,5* |
| row=4 | 4,1 | 4,2* | 4,3 | 4,4 | 4,5* |
| row=5 | 5,1 | 5,2* | 5,3 | 5,4 | 5,5* |
| row=6 | 6,1 | 6,2* | 6,3 | 6,4 | 6,5* |
| row=7 | 7,1* | 7,2* | 7,3* | 7,4* | 7,5* |

![](bbox=[0.6, 0.8, 0.85, 0.95])

# ProblemYBD: Write the logical condition for the following alphabet.

![](bbox=[0.1, 0.97, 0.45, 1.0])