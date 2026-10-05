# Example of Dynamic Allocation for a Two-Dimensional Array

A typical example of dynamic allocation is for the implementation of two-dimensional arrays. Let's write such a program using a pointer to pointer variable; you may find it useful for future reference, although this does not mean that the following approach is the most efficient. The next program reads the dimensions of a two-dimensional array at run-time, allocates memory for it, reads and stores them in its elements. The program emulates a dynamic two-dimensional array using one-dimensional dynamic arrays.

```
#include <iostream> // Example 14.5
using std::cout;
using std::cin;

void set_values(double **arr, int rows, int cols);

int main() {
    int i, rows, cols;
    double **arr; /* We use a pointer to pointer variable to handle the
two-dimensional array. */
    do {
        cout << "Enter entries of array [N][M]: ";
        cin >> rows >> cols;
    } while (rows <= 0 || cols <= 0);
    arr = new double*[rows]; /* Allocate memory for 'rows' pointers to
dbles. For example, if rows is 3, we allocate memory for arr[0], arr[1],
and arr[2] pointers. */
    for (i = 0; i < rows; i++) /* Allocate memory to store the elements of
each row. Each row contains 'cols' elements. */
        arr[i] = new double[cols];
    }
    set_values(arr, rows, cols);
    return 0;
}

void set_values(double **arr, int rows, int cols) {
    int i, j;
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            cout << "Set arr[" << i << \][" << j << "] = ";
            cin >> arr[i][j];
            cout << "arr[" << i << \][" << j << "] = " << arr[i][j] << '\n';
        }
    }
}
```

The program first creates an array of rows pointers, and for each it creates an array of cols elements. That is, arr[i] is a pointer to the row i that has cols doubles. The reason