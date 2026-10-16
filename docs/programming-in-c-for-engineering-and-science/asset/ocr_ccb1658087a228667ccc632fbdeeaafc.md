7. When using vectors of vectors, leave a space between the two > symbols. A common mistake is to forget this and to declare a vector of vectors with a statement like

```
vector<vector<int>> myGrid;
```

The compiler will read the >> as the input (or right-shift) operator, and because this makes no sense in this context, a compilation error will result. The correct approach is to leave a space:

```
vector<vector<int> > myGrid;
```

8. When processing the elements of a multidimensional array/vector using nested loops, the loops must be arranged so that the indices vary in the appropriate order. To illustrate, suppose that the two-dimensional array table is declared by

```
typedef int Array3x4 [3] [4];
Array3x4 table;
```

and the following data values are to be read into the array:

```
11 22 27 35 39 40 48 51 57 66 67 92
```

If these values are to be read and assigned in a row-wise manner so that the value is the matrix

```
11    22    27    35
39    40    48    51
57    66    67    92
```

then the following nested for loops are appropriate:

```
for (int row = 0; row < 3; row++)
    for (int col = 0; col < 4; col++)
        cin >> table[row][col];
```

If the order of these loops is reversed,

```
for (int col = 0; col < 4; col++)
    for (int row = 0; row < 3; row++)
        cin >> table[row][col];
```

then table will be loaded column-by-column, instead of row-by-row,

```
11  35  48  66
22  39  51  67
27  40  57  92
```

and operations applied to table will produce incorrect results.