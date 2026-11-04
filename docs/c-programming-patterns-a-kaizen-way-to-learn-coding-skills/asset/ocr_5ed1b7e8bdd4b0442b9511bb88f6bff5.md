# COLUMN LEVEL REPETITIVE ACTION

Let’s consider two attributes rows and columns of a 2-dimensional pattern as variables;

row → variable type of integer to store integer value one at a time and represents row number between 1 and 5.

col → variable type of integer to store integer value one at a time and represents column number between 1 and 5.

spaces → variable type of integer to store integer value one at a time and represents space character at column number between 1 and 5.

totalRows → variable type of integer to store integer value for total number of rows.

# Logic Trace Tables

| (row, col) value pair depicts the position of "*" character on the display screen |
|---|---|
| row=1, col=1 | row=1, col=2 | row=1, col=3 | row=1, col=4 | row=1, col=4 |
|  | row=2, col=2 | row=2, col=3 | row=2, col=4 | row=2, col=4 |
|  |  | row=3, col=3 | row=3, col=4 | row=3, col=4 |
|  |  |  | row=4, col=4 | row=4, col=4 |
|  |  |  |  | row=5, col=5 |

| Variable: row | Column level Repetitive Action | Expected Output |
|---|---|---|
|  | Variable: spaces | Variable: col | Character count | |
| 1 | 0(no space) | 1, 2, 3, 4, 5 | 4 Spaces + 1 star | * * * * * |
| 2 | 1 | 2, 3, 4, 5 | 3 Spaces + 2 stars | * * * * |
| 3 | 1,2 | 3, 4, 5 | 2 Spaces + 3 stars | * * * |
| 4 | 1,2,3 | 4, 5 | 1 Spaces + 4 stars | * * |
| 5 | 1,2,3,4 | 5 | 0 Spaces + 5 stars | * |

| Row level Repetitive Action | Expected Output |
| Variable: row | Column level Repetitive Action | |
|  | Variable: col | |
|  | Printing space character(s) | Printing star character(s) |
|  | min_val | max_val | min_val | max_val |
| 1 | 0 | 0 | 1 | 5 | * * * * * |
| 2 | 1 | 1 | 2 | 5 | * * * * |
| 3 | 1 | 2 | 3 | 5 | * * * |
| 4 | 1 | 3 | 4 | 5 | * * |
| 5 | 1 | 4 | 5 | 5 | * |

We know that totalRows = 5.

If we observe the numeric pattern for variable row (1, 2, 3, 4, and 5) is matching the numeric pattern of the column min_val of printing star character(s).

Our target is to express our program logic in terms of our chosen variables ( row, col, totalRows ).

Let’s use these variables to find generalised expression for printing star character(s).