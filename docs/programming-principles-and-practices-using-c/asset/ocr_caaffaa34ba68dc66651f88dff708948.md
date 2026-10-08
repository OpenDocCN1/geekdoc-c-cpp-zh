```
Matrix<int,2> a(3,4);
```

```
int s = a.size();          // number of elements
int d1 = a.dim1();         // number of elements in a row
int d2 = a.dim2();         // number of elements in a column
int* p = a.data();         // extract data as a pointer to a C-style array
```

We can ask for the total number of elements and the number of elements of each dimension. We can get a pointer to the elements as they are laid out in memory as a matrix.

We can subscript:

```
a(i,j);      // (i,j)th element (Fortran style), but range checked
a[i];        // ith row (C style), range checked
a[i][j];     // (i,j)th element (C style)
```

For a 2D **Matrix**, subscripting with **a[i]** yields the 1D **Matrix** that is the ith row. This means that we can extract rows and pass them to operations and functions that require a 1D **Matrix** or even a built-in array (**a[i].data()**). Note that **a(i,j)** may be faster than **a[i][j]**, though that will depend a lot on the compiler and optimizer.

![](bbox=[0.27, 0.5, 0.83, 0.59])

We can take slices:

```
a.slice(i);    // the rows from the a[i] to the last
a.slice(i,n);  // the rows from the a[i] to the a[i+n-1]
```

![](bbox=[0.26, 0.71, 0.83, 0.86])

Note that a slice of a 2D **Matrix** is itself a 2D **Matrix** (possibly with fewer rows).