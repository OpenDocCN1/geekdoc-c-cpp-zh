![](bbox=[0.199, 0.122, 0.897, 0.378])

**FIGURE 8-14** `sales[5][3]`

Suppose that:

```
int i = 5;
int j = 3;
```

Then, the previous statement:

```
sales[5][3] = 25.75;
```

is equivalent to:

```
sales[i][j] = 25.75;
```

So the indices can also be variables.

# Two-Dimensional Array Initialization during Declaration

Like one-dimensional arrays, two-dimensional arrays can be initialized when they are declared. The following example helps illustrate this concept. Consider the following statement:

```
int board[4][3] = {{2, 3, 1},
                    {15, 25, 13},
                    {20, 4, 7},
                    {11, 18, 14}};
```

This statement declares board to be a two-dimensional array of four rows and three columns. The elements of the first row are 2, 3, and 1; the elements of the second row are 15, 25, and 13; the elements of the third row are 20, 4, and 7; and the elements of the fourth row are 11, 18, and 14, respectively. Figure 8-15 shows the array board.