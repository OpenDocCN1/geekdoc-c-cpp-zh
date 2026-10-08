```
Matrix<double,2> ad2(n1);
// error: length of 2nd dimension missing
ad2(3) = 7.5;
// error: wrong number of subscripts
ad2(1,2,3) = 7.5;
// error: wrong number of subscripts

Matrix<double,3> ad3(n1,n2,n3);
Matrix<double,3> ad33(n1,n2,n3);
ad3 = ad33;
// OK: same element type, same dimensions
}
```

We catch mismatches between the declared number of dimensions and their use at compile time. Range errors we catch at run time and throw a **Matrix_error** exception.

The first dimension is the row and the second the column, so we index a 2D matrix (two-dimensional array) with (row,column). We can also use the [row] [column] notation because subscripting a 2D matrix with a single index gives the 1D matrix that is the row. We can visualize that like this:

![](bbox=[0.33, 0.41, 0.58, 0.52])

This **Matrix** will be laid out in memory in “row-first” order:

![](bbox=[0.25, 0.57, 0.65, 0.59])

A **Matrix** “knows” its dimensions, so we can address the elements of a **Matrix** passed as an argument very simply:

```
void init(Matrix<int,2>& a)
// initialize each element to a characteristic value
{
    for (int i=0; i<a.dim1(); ++i)
    for (int j = 0; j<a.dim2(); ++j)
    a(i,j) = 10*i+j;
}
```

```
void print(const Matrix<int,2>& a)
// print the elements row by row
{
    for (int i=0; i<a.dim1(); ++i) {
    for (int j = 0; j<a.dim2(); ++j)
    cout << a(i,j) <<'\t';
```