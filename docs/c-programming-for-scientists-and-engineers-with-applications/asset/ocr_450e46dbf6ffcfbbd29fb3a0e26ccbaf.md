# 476 Multidimensional Arrays

```
for(i = 0; i < IMAX; i++)
{
    for(j = 0; j < JMAX; j++)
{
        a[i][j] = 1.0;
    }
}
return 0;

```

Two-dimensional arrays may also be initialized by an explicit assignment. The following code shows such an assignment of values to the elements of the array.

```
float a[3][4];

a[0][0] = 2.5;
a[0][1] = 6.3;

...
a[2][2] = 16.8;
a[2][3] = 12.6;
```

This is not an efficient way to initialize two-dimensional arrays as it is not practical with large arrays.

> Programming Hint: For large arrays, use nested for loops to initialize array elements having the same initial value.

For large size arrays initialization during declaration and also by an explicit assignment is not practical unless they are initialized to zero or a scalar value. To initialize such arrays use an input statement as shown in the next section.

> Programming Hint: To store data in large size arrays use an input statement.

Arrays do not have to be processed by rows or columns. For example, in a square array the diagonal elements may be set to a certain value, the lower triangle elements set to a different value, and the upper triangle elements set to a third value.

```
#define IMAX 4
#define JMAX 4
```