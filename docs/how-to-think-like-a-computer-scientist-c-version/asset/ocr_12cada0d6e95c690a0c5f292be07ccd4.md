The first is a do-nothing constructor that makes a matrix with both dimensions 0. The second takes two integers, which are the initial number of rows and columns, in that order. The third is the same as the second, except that it takes an additional parameter that is used to initialize the elements of the matrix. The fourth is a copy constructor that takes another apmatrix as a row and column:

Just as with avectors, we can make apmatrix with any type of elements (including avectors, and even apmatrixes).
To access the elements, we use the [] operator to specify the row and column:

```
m2[0][0] = 1;
m3[1][2] = 10.0 * m2[0][0];
```

If we try to access an element that is out of range, the program prints an error message and quits.
The nrows and numcols functions get the number of rows and columns.
Remember that the row indices run from 0 to numrows( ) - 1 and the column indices run from 0 to numcols( ) - 1

The usual way to traverse a matrix is with a nested loop. This loop sets each element of the matrix to the sum of its two:

```
for (int row=0; row < m2.numrows(); row++) {
for (int col0=0; col < m2.numcols(); col++) {
m2[row][col] = row + col;
}
}
```

This loop prints each row of the matrix with tabs between the elements and newlines between the rows:

```
for (int row=0; row < m2.numrows(); row++) {
for (int col0=0; col < m2.numcols(); col++) {
cout << m2[row][col] << "\t";
cout << endl;
}
```

# 15.8 A distance matrix

Finally, we are ready to put the data from the file into a matrix. Specifically, the matrix will have one row and one column for each city.
'll create the matrix in main, with plenty of space to spare:

```
apmatrix<int> distances (50, 50, 00);
```