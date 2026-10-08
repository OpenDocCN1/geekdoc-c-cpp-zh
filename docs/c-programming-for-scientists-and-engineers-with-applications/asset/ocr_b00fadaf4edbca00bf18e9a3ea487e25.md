# Pointers and Dynamic Storage

Storage allocation:

| Address | Pointer |
|---|---|
| 1000 | aprtr + 0 |
| 1004 | aprtr + 1 |
| 1008 | aprtr + 2 |
| 1012 | aprtr + 3 |
| 1016 | aprtr + 4 |
| 1020 | aprtr + 5 |
| 1024 | aprtr + 6 |
| 1028 | aprtr + 7 |
| 1032 | aprtr + 8 |
| 1036 | aprtr + 9 |
| 1040 | aprtr + 10 |
| 1044 | aprtr + 11 |

Notice in this case a block of storage is allocated. The block consists of IMAX * JMAX cells and the size of each cell is the number of bytes of the data type for which the dynamic storage is allocated. For int and float data types the cell size is four bytes. The dynamic pointer aprtr points to the block of storage containing 12 storage cells of int type where each cell is four longs. The input/output, assignment, and arithmetic operations may be performed on dynamic storage through the dynamic pointer aprtr. The way the storage is handled in the program determines whether the array is one- or two-dimensional and which elements belong to the same row or the same column of the two-dimensional array.

If aprtr points to the beginning of a block of dynamic storage that will hold 12 elements, then the storage can be interpreted as a 3 × 4 array as follows:

| | | | |
|---|---|---||
| aprtr + 0 | aprtr + 3 |
| aprtr + 4 | aprtr + 7 |
| aprtr + 8 | aprtr + 11 |

In this, the element $A_{23}$ has the address aprtr + JMAX * $(i - 1) + (j - 1)$ where i is 2 and j is 3 and JMAX is 4.

The same block of storage can be interpreted as a 4 × 3 array, a 2 × 6 array, or a 6 × 2 array. If the array is processed sequentially by rows, it is not necessary