# 9.6 Different C# arrays

The following are various types of C# arrays that are used for developing code.

# Multi-dimensional arrays

A multi-dimensional array stores data in **more than one row dimension**. It is also known as rectangular array. User can declare two-dimensional array of integer as:

```
int [ , ] no;
```

A two-dimensional array can be considered as table. It has x rows and y columns. A two-dimensional array contains 2 rows and 4 columns.

|  | Column 0 | Column 1 | Column 2 | Column 3 |
|---|---|---|---|---|
| Row 0 | x[0][0] | x[0][1] | x[0][2] | x[0][3] |
| Row 1 | x[1][0] | x[1][1] | x[1][2] | x[1][3] |

# Initializing two dimensional arrays

The following array has 3 rows and 3 columns.

```
int [ , ] x = int [ 3, 3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

# Accessing elements of multidimensional array

An element from the multi dimensional array can be accessed using the subscripts. They are row and column index of the array.

# Example: