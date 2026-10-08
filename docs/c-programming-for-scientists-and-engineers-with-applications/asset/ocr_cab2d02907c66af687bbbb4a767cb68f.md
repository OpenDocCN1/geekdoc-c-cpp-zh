All of the elements of the array can be accessed by columns as follows:

```
for(j = 0; j < JMAX; j++)
{
    for(i = 0; i < IMAX; i++)
    {
        ...a[i][j]...
    }
}
```

A single element of the array can be accessed as follows:

```
a[2][3] /* refers to the element in the third row and the fourth column */
```

# 8.1.2 Storage Allocation

The storage for the array is determined when an array declaration statement is compiled. The number of storage cells needed is the product of the number of rows and the number of columns specified in the declaration. The size of each storage cell is determined by the data type of the array. This is compile-time storage and once storage is allocated during the loading of the program, the storage is dedicated to the array until the program terminates. If the array is too small, the defined constants that specify the size of the array need to be changed and the program must be recompiled after the change. Since storage is one-dimensional and sequential in order, the array elements are allocated sequential storage. In C the elements of a two-dimensional array are stored sequentially in row-major order, meaning that they are stored by rows.

The storage arrangement shown in this example uses the array subscript, also called the array indices.

Array declaration: int a[3][4];

Array elements:

| a[0][0] a[0][1] a[0][2] a[0][3] |
| a[1][0] a[1][1] a[1][2] a[1][3] |
| a[2][0] a[2][1] a[2][2] a[2][3] |