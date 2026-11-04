# COLUMN LEVEL REPETITIVE ACTION

| Row level Repetitive Action | Expected Output |
|---|---|
| row | Column level Repetitive Action | |
| | lower_limit <=spaces<= upper_limit | upper_limit >=num >= lower_limit |
| | lower_limit | upper_limit | | |
| 1 | 1 | 4 | 1 | 1 | 1 |
| 2 | 1 | 3 | 2 | 1 | 2 2 |
| 3 | 1 | 2 | 3 | 1 | 3 3 3 |
| 4 | 1 | 1 | 4 | 1 | 4 4 4 4 |
| 5 | 1 | 0 | 5 | 1 | 5 5 5 5 5 |

The lower_limit for spaces & num variable has the same numeric value expression for all the rows.

It’s consistent for all the rows. Likewise we need to come out with such a consistent expression for upper_limit for which it should suit any number of rows.

The other remaining variables are row & totalRows=5. Let’s try get generalised logical condition using these variables.

| Column level Repetitive Action | |
|---|---|
| row | lower_limit <=spaces<= upper_limit | upper_limit >=num >= lower_limit |
| | lower_limit | upper_limit | upper_limit | lower_limit |
| | | default | 1 | 2 | default | 1 | |
| 1 | 1 | 4 | totalRows - 1 | totalRows - row | 1 | row | 1 |
| 2 | 1 | 3 | totalRows - 2 | totalRows - row | 2 | row | 1 |
| 3 | 1 | 2 | totalRows - 3 | totalRows - row | 3 | row | 1 |
| 4 | 1 | 1 | totalRows - 4 | totalRows - row | 4 | row | 1 |
| 5 | 1 | 0 | totalRows - 5 | totalRows - row | 5 | row | 1 |

So the upper_limit of spaces & num variables are generalised.

The lower_limit & upper_limit are consistent for all the rows. It’s now generalised for n number of rows.

So our If-condition( lower_limit <=spaces<= upper_limit) becomes

```
1 <= spaces <= (totalRows – row)
```

The If-condition( upper_limit >=num >= lower_limit) becomes

```
row >=num >= 1
```

So it has two repetition process one for printing spaces and second for printing numeric values.

It means it requires two inner for-loops (nested for – loops).