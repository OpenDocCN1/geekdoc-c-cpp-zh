# ExerciseYBJ: Alphabet J

Let fill * characters in the first row & in the middle column. So matching logical conditions will be (row==1) || (col==3). We have used logical OR (||) conditional operator to add more * characters.

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1\* | 1,2\* | 1,3\* | 1,4\* | 1,5\* |
| row=2 | 2,1 | 2,2 | 2,3\* | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2 | 3,3\* | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2 | 4,3\* | 4,4 | 4,5 |
| row=5 | 5,1 | 5,2 | 5,3\* | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2 | 6,3\* | 6,4 | 6,5 |
| row=7 | 7,1 | 7,2 | 7,3\* | 7,4 | 7,5 |

Since we have to restrict column count to 3 at row=7, so we have to used logical AND **(&& col<=3)** conditional operator. Now adding logical condition **(row==7 && col<=3)** to previous conditions using logical OR (||) conditional operator will give * character set can be shown in the box. The logical condition becomes

**(row==1) || (col==3) || (row==7 && col<=3)**

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1\* | 1,2\* | 1,3\* | 1,4\* | 1,5\* |
| row=2 | 2,1 | 2,2 | 2,3\* | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2 | 3,3\* | 3,4 | 3,5 |
| row=4 | 4,1 | 4,2 | 4,3\* | 4,4 | 4,5 |
| row=5 | 5,1 | 5,2 | 5,3\* | 5,4 | 5,5 |
| row=6 | 6,1 | 6,2 | 6,3\* | 6,4 | 6,5 |
| row=7 | **7,1\*** | **7,2\*** | **7,3\*** | 7,4 | 7,5 |

# Please Pay Attention

Using logical AND we have restricted or limited the placing of * character at row=7. The condition used is (row==7 && col<=3).

If condition were row==7 only, then the complete row=7 would have then got filled with * characters. The additional condition &&col<=3 in the expression (row==7 && col<=3) actually limited the * characters in the row=7, started from column 1 till column 3.

Again, adding condition to previous (col==1 && row>=4).

The selected * character set shown with thick border is representing condition (col==1 && row>=4).

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1\* | 1,2\* | 1,3\* | 1,4\* | 1,5\* |
| row=2 | 2,1 | 2,2 | 2,3\* | 2,4 | 2,5 |
| row=3 | 3,1 | 3,2 | 3,3\* | 3,4 | 3,5 |
| row=4 | **4,1\*** | 4,2 | 4,3\* | 4,4 | 4,5 |
| row=5 | **5,1\*** | 5,2 | 5,3\* | 5,4 | 5,5 |
| row=6 | **6,1\*** | 6,2 | 6,3\* | 6,4 | 6,5 |
| row=7 | **7,1\*** | **7,2\*** | 7,3\* | 7,4 | 7,5 |

# Please Pay Attention

Using logical AND we have restricted or limited the placing of * character at col=1. The condition is (col=1 && row>=4).

If condition were col==1 only, then the complete col=1 would have then get filled with * characters.

The additional condition &&row>=4 in the expression (col==1 && row>=4) actually limited the * characters at the column 1 started from row 4 till row 7.