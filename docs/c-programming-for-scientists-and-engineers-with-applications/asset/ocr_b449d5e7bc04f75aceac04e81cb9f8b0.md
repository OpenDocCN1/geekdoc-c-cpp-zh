# 8.4 Manipulation of Arrays 485

# After

| value1 | value2 |
| --- | --- |
| 12.34 15.34 19.90 18.67 | 12.34 15.34 19.90 18.67 |
| 10.90 12.65 18.67 14.78 | 10.90 12.65 18.67 14.78 |
| 56.23 76.45 19.81 67.23 | 56.23 76.45 19.81 67.23 |

Notice that the values of the elements of the array value2 are assigned to the elements of the array value element-by-element in row order. This is the most efficient order for processing the arrays. Notice also that the arrays must be the same size and shape. The contents of the elements of array value2 do not change.

A specific row of one array may be assigned to a specific row of another array. For example the code to assign the third row of array value2 to the second row of array value1 as follows:

```
#define IMAX 10
#define JMAX 20

int main() {
    float value1[IMAX][JMAX], value2[IMAX][JMAX];
    int i, j;
    .
    for(j = 0; j < JMAX; j++) {
        value1[1][j] = value2[2][j];
    }
    return 0;
}
```

# Before

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

# After

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| 11.25 13.04 19.81 10.56 | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |