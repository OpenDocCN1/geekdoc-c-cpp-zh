Notice that the values of the third row from array value2 are copied to the second row of array value1, replacing the original values.

A specific column of one array may be assigned to a specific column of another array. For example, the code to assign the fourth column of array value2 to the second column of array value1 is as follows:

```
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

# Before

| value1 | value2 |
| --- --- --- --- --- --- --- --- |
| uuuu uuuu uuuu uuuu | 12.34 15.34 19.90 18.67 |
| uuuu uuuu uuuu uuuu | 10.90 12.65 18.67 14.78 |
| uuuu uuuu uuuu uuuu | 11.25 13.07 19.81 10.56 |

# After

| value1 | value2 |
| --- --- --- --- --- --- --- --- |
| uuuu uuuu uuuu uuuu | 12.34 15.34 19.90 18.67 |
| uuuu uuuu uuuu uuuu | 10.90 12.65 18.67 14.78 |
| uuuu uuuu uuuu uuuu | 11.25 13.07 19.81 10.56 |

Notice that the values of the fourth column from array value2 are copied to the second column of array value1, replacing the original values.

# 8.4.2 Array Arithmetic

The arithmetic operations of addition, subtraction, multiplication, and division applied to arrays are performed element-by-element using nested loops. The arrays must be of the same size and shape. The following example shows the addition operation.