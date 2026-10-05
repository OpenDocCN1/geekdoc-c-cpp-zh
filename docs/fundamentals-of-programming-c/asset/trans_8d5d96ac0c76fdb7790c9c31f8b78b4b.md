

```cpp
// 记录运行耗时

// 考虑的最大潜在素数
// const int MAX = 500000;
const int MAX = 500;

// 布尔型数组中的每个位置表示
// 该位置对应的数字不是素数；
// false 表示“素数”，true 表示“合数”。
// 初始所有数字都是素数，除非被证明不是
bool nonprimes[MAX]; // 全局数组，初始化为全零

int main() {
    clock start_time = clock(); // 记录开始时间
    // 第一个素数是 2；0 和 1 不是素数
    nonprimes[0] = true;

    // 从第一个素数 2 开始。
    for (int i = 2; i < MAX; i++) {
        if (!nonprimes[i]) {
            cout << i << ", \n            // 它是素数，所以消除它所有的
            // 不可能是素数的倍数
            for (int j = i+2; j < MAX; j += i)
                nonprimes[j] = true;
        }
    }
    cout << endl; // 光标移下一行
    // 打印经过的时间：
    cout << "Elapsed time: "
         << static_cast<double>(clock() - start_time)/CLOCKS_PER_SEC
         << " seconds" << endl;
}
```

列表 8.8 (measuresprimespeed.cpp) 也打印高达 500,000 的所有素数。使用归约（第 8.4 节），列表 8.8 (measuresprimespeed.cpp) 花了 77 秒。相比之下，列表 F4 (fasterprimespeed.cpp) 在系统上执行相同任务大约需要两秒。这与平方根版本的列表 8.5 (moreefficientprimes.cpp) ，后者运行需要两秒。如果目标是打印到 1,000,000 的素数，原始版本平均需要 271 秒，或大约四分半。平方根版本平均需要 4.5 秒。新的基于数组的版本平均需要 25 秒。对于 5,000,000，优化后的原始版本需要超过 1 小时 33 分钟，平方根版本需要可观的 39 秒，但数组版本平均运行需要 9 秒。

## F.4 多维数组

我们到目前为止的数组都是一维的——值的简单序列。C++ 支持高维数组。二维数组是一个用行和列可视化的内存块。该语句

## F.4. 多维数组

```cpp
int a[2][3];
```

将 `a` 声明为一个整数的二维（2D）数组。二维数组有时被称为矩阵。在这种情况下，该声明指定数组包含两行和三列。图 F.4 显示了由以下代码序列创建的数组的逻辑结构：

```cpp
int a[2][3]; // a 是一个二维数组
a[0][0] = 5;
a[0][1] = 19;
a[0][2] = 3;
a[1][0] = 22;
a[1][1] = -8;
a[1][2] = 10;
```

| | 5 | 19 | 3 |
|---|---|---|---|
| 1 | 22 | -8 | 10 |
| | 0 | 1 | 2 |

图 F.4：一个 2 × 3 二维数组

二维数组被称为 2 × 3 数组，意味着它有两行和三列（如图 F.4 所示）。行水平排列，列中的值垂直排列。在上面的每个赋值语句中，例如

```cpp
a[1][0] = 22;
```

第一个索引 (1) 表示行，第二个索引（这里为 0）表示数组内元素的列。

使用初始化一维数组列表的语法，可以这样声明并创建上述的二维数组 `a`：

```cpp
int a[2][3] = { { 5, 19, 3 }, { 22, -8, 10 } };
```

注意每个数组都有自己的大括号，且每行看起来都像 1D 数组初始化列表。你可以省略第一个索引，如下：

```cpp
int a[][3] = { { 5, 19, 3 }, { 22, -8, 10 } };
```

## F4. 多维数组

对于以这种方式初始化的二维数组，第一个下标是可选的，但第二个下标（即即每列的大小）是必须的。

要访问二维数组的元素，使用两个下标：

```cpp
a[r][c] = 4;                                // 给 r 行第 c 列的元素赋值
cout << a[m][n] << endl;                     // 显示 m 行第 n 列的元素
```

以下函数打印一个 ROWS x COLUMNS 的双浮点数二维数组的内容：

```cpp
void print (const double [ROWS][COLUMNS]) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
    }
}
```

参数 `m` 的声明相当复杂。我们可以通过 C++ 的 `typedef` 来简化语法。该语句

```cpp
typedef Matrix [ROWS][COLUMNS];
```

定义了一个新名称 `Matrix`。如果你在语句中使用 `typedef` 单词，它定义了一个二维数组 `Matrix` 的声明。`typedef` 关键字改变了语句的含义，因此它不是声明变量，而是定义一个类型。`typedef` 语句通常出现在源文件的顶部，并且通常具有全局作用域。在函数体内看到局部 `typedef` 是不常见的。

鉴于 `typedef` 语句定义了新类型名 `Matrix`，`print` 函数的参数可以更简单地表示：

```cpp
void print (const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
}
```

列表 F.5 (twodimarray.cpp) 对二维数组进行了实验，并利用 `typedef` 简化了代码。

列表 F.5: twodimarray.cpp
```cpp
#include <iostream>
#include <iomanip>
using namespace std;
const int ROWS = 3,
COLUMNS = 5;

// 名称 Matrix 代表一个新类型
// 它意味着一个 ROWS x COLUMNS
// 的双精度
// 浮点数二维数组
typedef double Matrix[ROWS][COLUMNS];

// 允许用户输入矩阵元素
void populate_matrix(Matrix m) {
    cout << "输入矩阵的 " << ROWS << " 行。" << endl;
    for (int row = 0; row < ROWS; row++) {
        cout << "Row " << row << " enter (" << COLUMNS << " values):";
        for (int col = 0; col < COLUMNS; col++) {
            cin >> m[row][col];
        }
    }
}

void print_matrix(const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
    }
}

int main() {
    Matrix mat;
    // 填充数组
    populate_matrix(mat);
    // 打印数组
    print_matrix(mat);
}
```

## F.5 指针与数组

列表 F.6: pointerprint.cpp
```cpp
#include <iostream>

using namespace std;

int main() {
    int a[] = { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 },
        *p;

    p = &a[0]; // p指向数组的第一个元素

    // 打印数组的内容
    for (int i = 0; i < 10; i++) {
        cout << *p << ' '; // 打印元素 p
        p++; // 增加 p 以指向下一个元素
    }
    cout << endl;
}
```

