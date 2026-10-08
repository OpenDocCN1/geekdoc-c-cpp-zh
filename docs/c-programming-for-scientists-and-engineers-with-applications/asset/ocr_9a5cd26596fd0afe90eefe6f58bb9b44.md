# 8.4 Manipulation of Arrays 489

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

These operations are performed element-by-element.

Matrix Transpose:

Interchanging the rows and columns of a matrix is called a matrix transpose. The following code shows the matrix transpose.

```
#define IMAX 3
#define JMAX 5

int main() 
{
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

Before:

| Matrix a |
| 4 2 3 1 0 |
| 5 6 4 8 9 |
| 9 3 7 2 8 |