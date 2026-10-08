

## 8.4 数组操作

### 之后

| value1 | value2 |
| --- | --- |
| 12.34 15.34 19.90 18.67 | 12.34 15.34 19.90 18.67 |
| 10.90 12.65 18.67 14.78 | 10.90 12.65 18.67 14.78 |
| 56.23 76.45 19.81 67.23 | 56.23 76.45 19.81 67.23 |

注意，数组 `value2` 的元素值按行顺序逐元素赋值给数组 `value1` 的元素。这是处理数组最高效的顺序。同样注意，数组必须具有相同的大小和形状。数组 `value2` 元素的内容不会改变。

可以将一个数组的特定行赋值给另一个数组的特定行。例如，将数组 `value2` 的第三行赋值给数组 `value1` 的第二行的代码如下：

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

### 之前

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### 之后

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

注意，数组 `value2` 的第三行的值被复制到数组 `value1` 的第二行，替换了原始值。可以将一个数组的特定列赋值给另一个数组的特定列。例如，将数组 `value2` 的第四列赋值给数组 `value1` 的第二列的代码如下：

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

### 之前

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### 之后

| value1 | value2 |
| --- | --- |
| uuu uuu uuu uuu | 12.34 15.34 19.90 18.67 |
| uuu uuu uuu uuu | 10.90 12.65 18.67 14.78 |
| uuu uuu uuu uuu | 11.25 13.07 19.81 10.56 |

### 8.4.2 数组算术

应用于数组的加、减、乘、除算术操作是通过嵌套循环逐元素执行的。数组必须具有相同的大小和形状。示例展示了加法：

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

注意，`a` 逐元素加到数组 `b`，结果存储在数组 `c` 中。减法、乘法和除法操作类似。

### 8.4.3 矩阵操作

在矩阵上定义的加减法与数组算术相同，都是逐元素执行的，但矩阵乘法是一种特殊操作。两个相同大小和形状的矩阵可以逐元素进行加减。矩阵转置、求逆以及以下示例展示了对矩阵的操作：

```c
#define IMAX 3
#define JMAX 5

int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
int i, j, k;
```

初始值：

| 矩阵 a | 矩阵 b |
|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 |
| 5 6 4 8 9 | 7 4 3 9 6 |
| 9 3 7 2 8 | 5 9 2 4 |

加法：
`c = a + b` 的实现如下：

```c
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] + b[i][j];
    }
}
```

| 矩阵 a | 矩阵 b | 矩阵 c |
|---|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 | 13 4 8 4 1 |
| 5 6 4 8 9 | 7 4 3 9 6 | 12 10 7 17 15 |
| 9 3 7 2 8 | 5 9 2 4 | 14 12 9 6 12 |

减法：
`c = a - b` 的实现如下：

```c
for(i = 0; i < IMAX; i++) {
    for(j = 0; j < JMAX; j++) {
        c[i][j] = a[i][j] - b[i][j];
    }
}
```

| 矩阵 a | 矩阵 b | 矩阵 c |
|---|---|---|
| 4 2 3 1 0 | 9 2 5 3 1 | -5 0 -2 -2 -1 |
| 5 6 4 8 9 | 7 4 3 9 6 | -2 2 1 -1 3 |
| 9 3 7 2 8 | 5 9 2 4 | 4 -6 5 -2 4 |

转置：
交换矩阵的行和列称为矩阵转置。以下代码展示了矩阵转置：

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

| 矩阵 a | 矩阵 b |
|---|---|
| 4 2 3 1 0 | 4 5 9 |
| 5 6 4 8 9 | 2 6 3 |
| 9 3 7 2 8 | 1 4 7 |

乘法：
如果第一个矩阵的列数等于第二个矩阵的行数，则定义它们的乘积。结果矩阵的大小为第一个矩阵的行数乘以第二个矩阵的列数。以下程序展示了两个矩阵的乘法：

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

注意，在这种情况下，矩阵 $y$ 是 $2 \times 3$，矩阵 $z$ 是 $3 \times 2$，因此它们可以进行乘法。

### 8.4.4 复习习题

- 1. 判断下列陈述对错。
  a. 在 C 语言中，可以通过名称将二维数组赋值另一个另一个相同的二维数组。
  b. 在 C 语言中，可以使用 for 循环将二维数组的一行赋值给另一个二维数组的行。
  c. 二维数组的算术操作可以通过数组名称执行。

