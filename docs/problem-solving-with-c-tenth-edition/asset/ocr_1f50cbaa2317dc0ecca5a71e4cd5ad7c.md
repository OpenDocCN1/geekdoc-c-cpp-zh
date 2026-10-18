rows is the number of rows desired in the two-dimensional array.
columns is the number of columns desired in the two-dimensional array.
Return value: a pointer to a one-dimensional dynamic array large enough to hold a two-dimensional array of size rows * columns.

Note that int ptr = create2DArray(2,3); would create an array analogous to that created by int ptr[2][3];

```
void set(int *arr, int rows, int columns,
    int desired_row, int desired_column, int val);
```

This stores val into the emulated two-dimensional array at position desired_row, desired_column. The function should print an error message and exit if the desired indices are invalid.

arr is the one-dimensional array used to emulate a two-dimensional array.
rows is the total number of rows in the two-dimensional array.
columns is the total number of columns in the two-dimensional array.
desired_row is the zero-based index of the row the caller would like to access.
desired_column is the zero-based index of the column the caller would like to access.
val is the value to store at desired_row and desired_column.

```
int get(int *arr, int rows, int columns,
    int desired_row, int desired_column);
```

This returns the value in the emulated two-dimensional array at position desired_row, desired_column. The function should print an error message and exit if the desired indices are invalid.

arr is the one-dimensional array used to emulate a two-dimensional array.
rows is the total number of rows in the two-dimensional array.
columns is the total number of columns in the two-dimensional array.
desired_row is the zero-based index of the row the caller would like to access.
desired_column is the zero-based index of the column the caller would like to access.

Create a suitable test program that invokes all three functions.

8. Many theatres contain seating which can be removed or rearranged depending on the performance. Write a program which uses a