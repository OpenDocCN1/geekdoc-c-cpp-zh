We know that totalRows = 5 .

The column **min_val** for printing star character(s) can be given as;

| Row level Repetitive Action (Variable : row) | Column level Repetitive Action (Variable : col) | Printing space character(s) min_val | Printing space character(s) max_val (default) | Printing star character(s) min_val | Printing star character(s) max_val |
|---|---|---|---|---|---|
| 1 | | 1 | 4 | 5 - 0 | totalRows |
| 2 | | 1 | 3 | 5 - 1 | totalRows |
| 3 | | 1 | 2 | 5 - 2 | totalRows |
| 4 | | 1 | 1 | 5 - 3 | totalRows |
| 5 | | 0 | 0 | 5 - 4 | totalRows |

If we can try variable totalRows to generalise the numeric pattern of the column **min_val** .

Then it will be totalRows – 0 , totalRows – 1,...so on. The part of this expression nearly following the numeric pattern of the variable row = 1,2,...5.The former is having the numeric pattern starting from zero(0) and row variable's numeric pattern starting from one(1).Let it be ,start the numeric pattern of row variable too start from zero(0).

Let's make use of the variables <u>totalRows</u> & <u>row</u> to derive the generalised expression for printing star character(s).

| Row level Repetitive Action (Variable : row) | Column level Repetitive Action (Variable : col) | Printing space character(s) min_val | Printing space character(s) max_val (default) | Printing star character(s) min_val | Printing star character(s) max_val |
|---|---|---|---|---|---|
| 0 | | 1 | 4 | totalRows - 0 | totalRows |
| 1 | | 1 | 3 | totalRows - 1 | totalRows |
| 2 | | 1 | 2 | totalRows - 2 | totalRows |
| 3 | | 1 | 1 | totalRows - 3 | totalRows |
| 4 | | 0 | 0 | totalRows - 4 | totalRows |

We can use the variable **row** to generalise the column **min_val** for printing star character(s).