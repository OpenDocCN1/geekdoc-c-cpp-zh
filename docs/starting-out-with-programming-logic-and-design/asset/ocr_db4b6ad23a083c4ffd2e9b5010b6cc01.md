# Declaring a Two-Dimensional Array

To declare a two-dimensional array, two size declarators are required: The first one for the number of rows and the second one for the number of columns. The following pseudocode shows an example of how to declare a two-dimensional array:

```
Declare Integer values[3][4]
```

This statement declares a two-dimensional array with three rows and four columns. The name of the array is values, and there are a total of twelve elements in the array. With one-dimensional arrays, it is best to use named constants for the size declarators. Here is an example:

```
Constant Integer ROWS = 3
Constant Integer COLS = 4
Declare Integer values[ROWS][COLS]
```

When processing the data in a two-dimensional array, each element has two subscripts: one for its row and another for its column. The array elements in row 0 are referenced as follows:

```
values[0][0]
values[0][1]
values[0][2]
values[0][3]
```

The elements in row 1 are as follows:

```
values[1][0]
values[1][1]
values[1][2]
values[1][3]
```

The elements in row 2 are as follows:

```
values[2][0]
values[2][1]
values[2][2]
values[2][3]
```

Figure 8-18 illustrates the array with the subscripts shown for each element.

# Figure 8-18 Subscripts for each element of the values array

| Column 0 | Column 1 | Column 2 | Column 3 |
|---|---|---|---||
| Row 0 | values[0][0] | values[0][1] | values[0][2] | values[0][3] |
| Row 1 | values[1][0] | values[1][1] | values[1][2] | values[1][3] |
| Row 2 | values[2][0] | values[2][1] | values[2][2] | values[2][3] |