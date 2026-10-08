# Initial Values:

Matrix a Matrix b

| 4 | 2 | 3 | 0 | 9 | 2 | 5 | 1 |
| 5 | 6 | 4 | 8 | 7 | 4 | 3 | 9 |
| 9 | 3 | 7 | 2 | 5 | 9 | 4 | 7 |

Addition:
c = a + b is implemented as:

```
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] + b[i][j];
    }
}
```

Matrix a Matrix b Matrix c

| 4 | 2 | 3 | 0 | 9 | 2 | 5 | 1 | 13 | 4 | 8 | 4 | 1 |
| 5 | 6 | 4 | 8 | 7 | 4 | 3 | 9 | 12 | 10 | 7 | 17 | 15 |
| 9 | 3 | 7 | 2 | 5 | 9 | 4 | 7 | 14 | 12 | 9 | 6 | 15 |

Subtraction:
c = a - b is implemented as:

```
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] - b[i][j];
    }
}
```