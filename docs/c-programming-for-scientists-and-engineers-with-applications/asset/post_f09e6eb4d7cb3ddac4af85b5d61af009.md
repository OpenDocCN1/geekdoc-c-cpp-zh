
## 8.4 Manipulation of Arrays

### After

| value1 | value2 |
| --- | --- |
| 12.34 15.34 19.90 18.67 | 12.34 15.34 19.90 18.67 |
| 10.90 12.65 18.67 14.78 | 10.90 12.65 18.67 14.78 |
| 56.23 76.45 19.81 67.23 | 56.23 76.45 19.81 67.23 |

Notice that the values of the elements of the array value2 are assigned to the elements of the array value element-by-element in row order. This is the most efficient order for processing the arrays. Notice also that the arrays must be the same size and shape. The contents of the elements of array value2 do not change.

A specific row of one array may be assigned to a specific row of another array. For example the code to assign the third row of array value2 to the second row of array value1 is as follows:

```c
#define IMAX 10
#define JMAX 20

int main() {
    float value1[IMAX][JMAX], value2[IMAX][JMAX];
    int i, j;
    for(j = 0; j < JMAX; j++) {
        value1[1][j] = value2[2][j];
    }
    return 0;
}
```

### Before

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### After

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

Notice that the values of the third row from array value2 are copied to the second row of array value1, replacing the original values. A specific column of one array may be assigned to a specific column of another array. For example, the code to assign the fourth column of array value2 to the second column of array value1 is as follows:

```c
#define IMAX 3
#define JMAX 4

int main() {
    float value1[IMAX][JMAX], value2[IMAX][JMAX];
    int i, j;
    for (i = 0; i < IMAX; i++) {
        value1[i][1] = value2[i][3];
    }
    return 0;
}
```

### Before

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### After

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### 8.4.2 Array Arithmetic

The arithmetic operations of addition, subtraction, multiplication, and division applied to arrays are performed element-by-element using nested loops. The arrays must be of the same size and shape. The following example shows addition:

```c
#include <stdio.h>
#define IMAX 3
#define JMAX 4

int main() {
    int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
    int i, j;
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            c[i][j] = a[i][j] + b[i][j];
        }
    }
    return 0;
}
```

| a | b | c |
|---|---|---|
| 12 | 18 | 30 |
| 13 | 20 | 33 |
| 18 | 24 | 42 |

Notice that a is added to array b element-by-element and the result is stored in array c. Subtraction, multiplication, and division operations are similar.

### 8.4.3 Matrix Operations

The addition and subtraction operations defined on matrices are the same as array arithmetic, which is carried out element-by-element, but matrix multiplication is a special operation. Two matrices of the same size and shape may be added or subtracted element-by-element. Matrix transpose, inverse, and the following examples show operations on matrices:

```c
#define IMAX 3
#define JMAX 5

int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
int i, j, k;
```

Initial Values:

| Matrix a | Matrix b |
|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 |
| 5 6 4 8 9 | 7 4 3 9 6 |
| 9 3 7 2 8 | 5 9 2 4 7 |

Addition:
c = a + b is implemented as:

```c
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] + b[i][j];
    }
}
```

| Matrix a | Matrix b | Matrix c |
|---|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 | 13 4 8 4 1 |
| 5 6 4 8 9 | 7 4 3 9 6 | 12 10 7 17 15 |
| 9 3 7 2 8 | 5 9 2 4 7 | 14 12 9 6 15 |

Subtraction:
c = a - b is implemented as:

```c
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] - b[i][j];
    }
}
```

| Matrix a | Matrix b | Matrix c |
|---|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 | -5 0 -2 -1 |
| 5 6 4 8 9 | 7 4 3 9 6 | -2 2 1 -1 3 |
| 9 3 7 2 8 | 5 9 2 4 7 | 4 -6 5 -2 1 |

These operations are performed element-by-element.

Matrix Transpose:

Interchanging the rows and columns of a matrix is called a matrix transpose. The following code shows the matrix transpose.

```c
#define IMAX 3
#define JMAX 5

int main() {
    int a[IMAX][JMAX], b[JMAX][IMAX];
    int i, j;
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            b[j][i] = a[i][j];
        }
    }
    return 0;
}
```

|::

| Matrix a |
| 4 2 3 1 0 |
| 5 6 4 8 9 |
| 9 3 7 2 8 |

| Matrix b |
| 9 2 5 3 1 |
| 7 4 3 9 6 |
| 5 9 2 4 7 |

| Matrix c |
| -5 0 -2 -1 |
| -2 2 1 -1 3 |
| 4 -6 5 -2 1 |

Matrix Multiplication:

The product of two matrices is defined if the number of columns of the first matrix is equal to the number of rows of the second matrix. The size of the resulting matrix is the number of rows of the first matrix by the number of columns of the second matrix. The following program shows the multiplication of two matrices:

```c
#include <stdio.h>
#define IMAX 3
#define JMAX 5
#define KMAX 4

int main() {
    int i, j, k, sum;
    int x[IMAX][JMAX], y[IMAX][KMAX], z[KMAX][JMAX];
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            sum = 0;
            for(k = 0; k < KMAX; k++) {
                sum = sum + y[i][k] * z[k][j];
            }
            x[i][j] = sum;
        }
    }
    return 0;
}
```

Notice in this case matrix $y$ is $2 \times 3$ and matrix $z$ is $3 \times 2$, therefore they can be multiplied.

### 8.4.4 Review Questions

- 1. Indicate whether the following statements are true or false.
  a. In C a two-dimensional array may be assigned to another two-dimensional array of the same size by name.
  b. In C a row of a two-dimensional array may be assigned to a row of another two-dimensional array using a for loop.
  c. Arithmetic operations on two-dimensional arrays may be performed by array name.
