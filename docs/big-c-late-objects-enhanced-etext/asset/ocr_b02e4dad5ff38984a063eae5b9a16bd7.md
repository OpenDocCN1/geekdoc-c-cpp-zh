# 6.6.5 Two-Dimensional Array Parameters

A two-dimensional array parameter must have a fixed number of columns.

When defining a function with a two-dimensional array parameter, you must specify the number of columns as a constant with the parameter type. For example, this function computes the total of a given row:

```
```c
const int COLUMNS = 3;

int row_total(int table[][COLUMNS], int row)
{
    int total = 0;
    for (int j = 0; j < COLUMNS; j++)
    {
        total = total + table[row][j];
    }
    return total;
}
```
```

This function can compute row totals of a two-dimensional array with an arbitrary number of rows, but the array must have 3 columns. You have to write a different function if you want to compute row totals of a two-dimensional array with 4 columns.

To understand this limitation, you need to know how the array elements are stored in memory. Although the array appears to be two-dimensional, the elements are still stored as a linear sequence. Figure 13 shows how the counts array is stored, row by row.

![](bbox=[0.299, 0.486, 0.694, 0.575])

**Figure 13**  A Two-Dimensional Array is Stored as a Sequence of Rows

For example, to reach

`counts[3][1]`

the program must first skip past rows 0, 1, and 2 and then locate offset 1 in row 3. The offset from the start of the array is

$$3 \times \text{number of columns} + 1$$

Now consider the row_total function. The compiler generates code to find the element

`table[i][j]`

by computing the offset

`i * COLUMNS + j`

The compiler uses the value that you supplied in the second pair of brackets when declaring the parameter:

```
```c
int row_total(int table[][COLUMNS], int row)
```
```

Note that the first pair of brackets should be empty, just as with one-dimensional arrays.