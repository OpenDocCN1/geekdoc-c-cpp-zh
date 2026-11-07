
当嵌套的 `for` 语句执行完毕时，`lowGrade` 包含二维数组中的最小成绩。函数 `maximum` 的工作方式与函数 `minimum` 类似。

### 函数 average

函数 `average`（第 72–81 行）接收两个参数——某个学生的测试成绩一维数组（`setOfGrades`）以及该数组中测试成绩的数量。第 33 行调用 `average` 时，第一个参数——`studentGrades[student]`——传递二维数组中某一行的地址。参数 `studentGrades[1]` 是数组第 1 行的起始地址。请记住，二维数组基本上是一维数组的数组，而一维数组的名称就是该数组在内存中的地址。函数 `average` 计算数组元素之和，用总和除以测试成绩数量，并返回浮点结果。

### 自测题

- **1.（这段代码做什么？）** 下面的嵌套 `for` 语句做什么？

```c
product = 1;

for (row = 0; row <= 2; ++row) {
    for (column = 0; column <= 3; ++column) {
        product *= m[row][column];
    }
}
```

  **答案：** 它计算 3×4 的 double 数组 `m` 中所有元素值的乘积。

- **2.（这段代码做什么？）** 下面的嵌套 `for` 语句做什么？

```c
// loop through rows of grades
for (i = 0; i < pupils; ++i) {
    // loop through columns of grades
    for (j = 0; j < tests; ++j) {
        if (grades[i][j] < lowGrade) {
            lowGrade = grades[i][j];
        }
    }
}
```

  **答案：** 它遍历一个二维数组 `grades`，该数组有 `pupils` 行和 `tests` 列，试图找出数组中的最低成绩。假设成绩范围为 0 到 100，则 `lowGrade` 需要初始化为 100 或更大的值。

## 6.12 变长数组

到目前为止，你定义的每个数组都在编译时指定了大小。但是，如果你直到执行时才能确定数组的大小，该怎么办？过去，为了处理这种情况，你必须使用动态内存分配（在第 12 章“数据结构”中介绍）。对于在编译时不知道数组大小的情况，C 提供了变长数组（VLA）——其长度由执行时求值的表达式决定。² 图 6.18 的程序声明并打印了几个 VLA。

```c
// fig06_18.c
// Using variable-length arrays in C99
#include <stdio.h>

// function prototypes
void print1DArray(size_t size, int array[size]);
void print2DArray(size_t row, size_t col, int array[row][col]);

int main(void) {
    printf("%s", "Enter size of a one-dimensional array: ");
    int arraySize = 0; // size of 1-D array
    scanf("%d", &arraySize);

    int array[arraySize]; // declare 1-D variable-length array

    printf("%s", "Enter number of rows and columns in a 2-D array: ");
    int row1 = 0; // number of rows in a 2-D array
    int col1 = 0; // number of columns in a 2-D array
    scanf("%d %d", &row1, &col1);

    int array2D1[row1][col1]; // declare 2-D variable-length array

    printf("%s", "Enter number of rows and columns in another 2-D array: ");
    int row2 = 0; // number of rows in a 2-D array
    int col2 = 0; // number of columns in a 2-D array
    scanf("%d %d", &row2, &col2);

    int array2D2[row2][col2]; // declare 2-D variable-length array

    // test sizeof operator on VLA
    printf("sizeof(array) yields array size of %zu bytes\n", sizeof(array));

    // assign elements of 1-D VLA
    for (size_t i = 0; i < arraySize; ++i) {
        array[i] = i * i;
    }

    // assign elements of first 2-D VLA
    for (size_t i = 0; i < row1; ++i) {
        for (size_t j = 0; j < col1; ++j) {
            array2D1[i][j] = i + j;
        }
    }

    // assign elements of second 2-D VLA
    for (size_t i = 0; i < row2; ++i) {
        for (size_t j = 0; j < col2; ++j) {
            array2D2[i][j] = i + j;
        }
    }

    puts("\nOne-dimensional array:");
    print1DArray(arraySize, array); // pass 1-D VLA to function

    puts("\nFirst two-dimensional array:");
    print2DArray(row1, col1, array2D1); // pass 2-D VLA to function

    puts("\nSecond two-dimensional array:");
    print2DArray(row2, col2, array2D2); // pass other 2-D VLA to function
}

void print1DArray(size_t size, int array[size]) {
    // output contents of array
    for (size_t i = 0; i < size; i++) {
        printf("array[%zu] = %d\n", i, array[i]);
    }
}

void print2DArray(size_t row, size_t col, int array[row][col]) {
    // output contents of array
    for (size_t i = 0; i < row; ++i) {
        for (size_t j = 0; j < col; ++j) {
            printf("%5d", array[i][j]);
        }

        puts("");
    }
}
```

```text
Enter size of a one-dimensional array: 6
Enter number of rows and columns in a 2-D array: 2 5
Enter number of rows and columns in another 2-D array: 4 3

sizeof(array) yields array size of 24 bytes

One-dimensional array:
array[0] = 0
array[1] = 1
array[2] = 4
array[3] = 9
array[4] = 16
array[5] = 25

First two-dimensional array:
 0 1 2 3 4
 1 2 3 4 5

Second two-dimensional array:
   0   1   2
   1   2   3
   2   3   4
   3   4   5
```

**图 6.18** | 在 C99 中使用变长数组。（第 3 部分，共 3 部分。）

### 创建 VLA

第 10–29 行提示用户输入一个一维数组和两个二维数组所需的大小，并使用第 14、21 和 29 行中的输入值创建 VLA。只要表示数组大小的变量是整数，这些行就是有效的。

### 用于 VLA 的 sizeof 运算符

创建数组后，我们在第 32–33 行使用 `sizeof` 运算符检查一维 VLA 的长度。`sizeof` 运算符通常是编译时操作，但当应用于 VLA 时，它在运行时操作。输出窗口显示，`sizeof` 运算符返回的大小为 24 字节——是我们输入数字的四倍，因为在我们机器上 `int` 的大小是 4 字节。

### 为 VLA 元素赋值

接下来，我们为 VLA 的元素赋值（第 36–52 行）。填充一维数组时，我们使用循环继续条件 `i < arraySize`。与定长数组一样，没有任何保护措施防止越出数组边界。

### 函数 print1DArray

第 64–69 行定义了函数 `print1DArray`，它显示其一维 VLA 参数。VLA 函数参数与常规数组参数具有相同的语法。我们在参数 `array` 的声明中使用了参数 `size`，但这纯粹是给程序员看的文档说明。

### 函数 print2DArray

函数 `print2DArray`（第 71–80 行）显示一个二维 VLA。回想一下，在多维数组参数中，除第一个下标外，必须为所有下标指定大小。同样的限制也适用于 VLA，不同之处在于大小可以由变量指定。传递给函数的 `col` 初始值决定了每一行在内存中的起始位置，就像定长数组一样。

### 自测题

- **1. *（正/误）*** 与定长数组不同，VLA 提供了防止越出数组边界的保护。

  **答案：** *错误。* 实际上，与定长数组一样，没有任何保护措施防止越出数组边界。

- **2. *（正/误）*** `sizeof` 是仅编译时操作。

  **答案：** *错误。* 实际上，通常 `sizeof` 是编译时操作，但当应用于 VLA 时，`sizeof` 在运行时操作。

## 6.13 安全的 C 编程

### 数组下标的边界检查

确保用于访问数组元素的每个下标都在数组边界内很重要。一维数组的下标必须大于或等于 0 且小于元素个数。二维数组的行下标和列下标必须分别大于或等于 0 且小于行数和列数。这也适用于具有更多维度的数组。

允许程序读取或写入数组边界之外的数组元素是常见的安全缺陷。读取越界数组元素可能导致程序崩溃，甚至可能在使用错误数据的情况下看起来执行正确。写入越界元素（称为缓冲区溢出）可能破坏程序在内存中的数据，导致程序崩溃，甚至允许攻击者利用系统并执行他们自己的代码。

C 不提供数组的自动边界检查。你必须确保数组下标始终大于或等于 0 且小于数组的元素个数。有关帮助防止此类问题的更多技术，请参见 CERT 指南 ARR30-C，网址为 https://wiki.sei.cmu.edu/confluence。

### scanf_s

边界检查在字符串处理中也很重要。将字符串读入 `char` 数组时，`scanf` 不会自动防止缓冲区溢出。如果输入的字符数大于或等于数组长度，`scanf` 会将字符——包括字符串的终止空字符（`'\0'`）——写到数组末尾之外。这可能覆盖内存中其他变量的值。此外，如果程序写入那些其他变量，它可能覆盖字符串的 `'\0'`。

函数通过查找字符串的终止 `'\0'` 字符来确定字符串在哪里结束。例如，回想一下，函数 `printf` 通过从内存中字符串的开头读取字符并继续，直到遇到字符串的 `'\0'` 来输出字符串。如果缺少 `'\0'`，`printf` 会继续从内存中读取（并打印），直到在内存中遇到后面的某个 `'\0'`。这可能导致奇怪的结果，或导致程序崩溃。

C11 标准的可选附录 K 提供了许多字符串处理和输入/输出函数的更安全版本。将字符串读入字符数组时，函数 `scanf_s` 执行检查以确保不会写到数组末尾之外。假设 `myString` 是一个 20 字符的数组，则语句

```c
scanf_s("%s", myString, 20);
```

将字符串读入 `myString`。函数 `scanf_s` 要求为格式字符串中的每个 `%s` 提供两个参数：
