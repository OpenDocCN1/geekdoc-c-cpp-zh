# Alternative solution2

Let’s start with the one of the logic trace table that we got from the previous solution.

| Row level Repetitive Action | Expected Output |
|---|---|
| Variable : row | Column level Repetitive Action |
|  | Variable : col |
|  | Printing space character(s) | Printing star character(s) |
|  | min_val | max_val | min_val | max_val |
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 1 | 2 | 8 | * * * * * * * |
| 5 | 0 | 0 | 1 | 9 | * * * * * * * * |
| 6 | 1 | 1 | 2 | 8 | * * * * * * * |
| 7 | 1 | 2 | 3 | 7 | * * * * |
| 8 | 1 | 3 | 4 | 6 | * * * |
| 9 | 1 | 4 | 5 | 5 | * |

Let’s focus our attention for printing of star character(s) and try to find out the expression in terms of the variables i.e. row & totalRows=5.

| Row level Repetitive Action | |
| Variable : row | Column level Repetitive Action |
|  | Variable : col |
|  | Printing star character(s) |
|  | min_val |  |  | max_val |  |  |
|  | default | 1 | 2 | default | 1 | 2 |
| 1 | 5 | 5-0 | totalRows +1 - 1 | 5 | totalRows +0 | totalRows +1 - 1 |
| 2 | 4 | 5-1 | totalRows +1 - 2 | 6 | totalRows +1 | totalRows +2 - 1 |
| 3 | 3 | 5-2 | totalRows +1 - 3 | 7 | totalRows +2 | totalRows +3 - 1 |
| 4 | 2 | 5-3 | totalRows +1 - 4 | 8 | totalRows +3 | totalRows +4 - 1 |
| 5 | 1 | 5-4 | totalRows +1 - 5 | 9 | totalRows +4 | totalRows +5 - 1 |
| 6 | 2 | 2 | 2 | 8 | totalRows +3 | totalRows +5 - 2 |
| 7 | 3 | 3 | 3 | 7 | totalRows +2 | totalRows +5 - 3 |
| 8 | 4 | 4 | 4 | 6 | totalRows +1 | totalRows +5 - 4 |
| 9 | 5 | 5 | 5 | 5 | totalRows +0 | totalRows +5 - 5 |

We can use row=1,2,3,4,5 values to partially express the columns min_val and max_val.

| Row level Repetitive Action | |
| Variable : row | Column level Repetitive Action |
|  | Variable : col |
|  | Printing star character(s) |
|  | min_val |  | max_val |  |  |
|  |  | 3 |  | 3 |  | 4 |
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 | totalRows + row - 1 |
| 6 | 2 | 2 | 8 | totalRows +5 - 2 | 2*totalRows - 2 |
| 7 | 3 | 3 | 7 | totalRows +5 - 3 | 2*totalRows - 3 |
| 8 | 4 | 4 | 6 | totalRows +5 - 4 | 2*totalRows - 4 |
| 9 | 5 | 5 | 5 | totalRows +5 - 5 | 2*totalRows - 5 |