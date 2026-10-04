
与一维数组一样，二维数组也可以通过循环（while 或 for）使用元素表示法来显示。程序 7.4 显示了一个 3x4 二维数组的所有元素，展示了这两种技术。注意使用常量来定义数组的行和列。

## 程序 7.4

```cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    const int NUMROWS = 3;
    const int NUMCOLS = 4;
    int i, j;
    int val[NUMROWS][NUMCOLS] = {8,16,9,52,3,15,27,6,14,25,2,10};

    cout << "\nDisplay of val array by explicit element\n";
    cout << endl << setw(4) << val[0][0] << setw(4) << val[0][1]
    cout << setw(4) << val[0][2] << setw(4) << val[0][3] << endl;
    cout << setw(4) << val[1][0] << setw(4) << val[1][1]
    cout << setw(4) << val[1][2] << setw(4) << val[1][3] << endl;
    cout << setw(4) << val[2][0] << setw(4) << val[2][1]
    cout << setw(4) << val[2][2] << setw(4) << val[2][3];

    cout << "\nDisplay of val array using a nested for loop\n";
    for (int i = 0; i < NUMROWS; i++) {
        cout << endl;
        for (int j = 0; j < NUMCOLS; j++) {
            cout << setw(4) << val[i][j];
        }
    }
    return 0;
}
```

这是程序 7.4 产生的输出：

```
Display of val array by explicit element
8 16 9 52
3 15 27 6
14 25 2 10
```

## 第 7 章 391

声明和处理二维数组

```
Display of val array using a nested for
8 16 9 52
3 15 27 6
14 25 2 10
```

程序 7.4 产生的 val 数组第一次显示是通过指定每个数组元素来构建的。数组元素值的第二次显示（与第一次相同）是通过使用嵌套的 for 循环产生的。在处理二维数组时，嵌套循环特别有用，因为它们允许程序轻松地指定并循环遍历元素。在程序 7.4 中，变量 `i` 控制外层循环，变量 `j` 控制内层循环。外层循环的每次通过对应一行，内层循环提供列元素。打印完完整的一行后，为下一行开始一个新行。结果是按行方式显示数组。

在分配二维元素后，就可以开始处理数组了。通常，使用循环来处理二维数组，因为之前提到的，它们允许程序轻松地指定并循环遍历每个数组元素。例如，程序 7.5 中的嵌套 for 循环用于将 `val` 中的每个元素乘以标量 10 并显示结果值。

## 程序 7.5

```cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    const int NUMROWS = 3;
    const int NUMCOLS = 4;
    int i, j;
    int val[NUMROWS][NUMCOLS] = {8,16,9,52,3,15,27,6,14,25,2,10};

    // 将每个元素乘以 10 并显示它
    cout << "\nDisplay of multiplied elements:\n";

    for (i = 0; i < NUMROWS; i++)
    {
        cout << endl;
        for (j = 0; j < NUMCOLS; j++)
        {
            val[i][j] = val[i][j] * 10;
            cout << setw(5) << val[i][j];
        } // 内层循环结束
    } // 外层循环结束
    return 0;
}
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_410_0.png)

## 392 数组

程序 7.5 产生的输出如下：

```
Display of multiplied elements
80 160 90 520
30 150 270 60
140 250 20 100
```

## 高维数组

超过两个维的数组并不常见；但 C++ 允许通过列出数组所有维度的最大大小来声明任意维。例如，`int response[4][10][6];` 声明了一个三维数组。数组中的第一个元素指定为 `response[0][0][0]`，最后一个元素指定为 `response[3][9][5]`。

如图 7.7 所示，你可以将三维数组想象成一本数据表书。使用这个类比，将第一个索引视为表格中所需行的位置，第二个索引视为所需的列，而第三个索引值（通常称为“秩”）视为所选表格的页码。

| 行索引 | 列索引 |
| --- | --- |

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_411_0.png)

图 7.7 三维数组的表示

同样，可以声明任何维度的数组。从概念上说，四维数组可以表示为一架书，第四维度用于声明书架上选定的书；五维数组可以看作是一个装满书的书柜，第五维度指向书柜中选定的书架。使用相同的类比，六维数组可以被视为一排书架，该维度指向该行中所需的书架；七维数组可以被视为多排书架，第七维度指向所需的行，依此类推。另一种观点，三、四、五、六等维的数组可以被视为阶为三、四、五、六等……的数学 $n$-元组。

## 第 7 章 393

声明和处理二维数组

## 练习题 7.3

- 1. （练习）为以下内容编写规格语句：
    a. 一个 6 行 10 列的整数数组
    b. 一个 2 行 5 列的整数数组
    c. 一个 7 行 12 列的字符数组
    d. 一个 15 行 7 列的字符数组
    e. 一个 10 行 25 列的双精度浮数数组
    f. 一个 16 行 8 列的双精度浮数数组

- 2. （纸上调试）确定后续程序产生的输出：
```cpp
#include <iostream>
using namespace std;

int main() {
    int i, j, val[3][4] = {8,16,9,52,3,15,27,6,14,25,2,10};
    for (i = 0; i < 3; i++) {
        cout << endl;
        for (j = 0; j < 4; j++) {
            cout << setw(4) << val[i][j];
        }
    }
    return 0;
}
```

- 3. （练习）编写一个 C++ 程序，累加 val 数组中的每个元素并显示总和。
    b. 修改第 3 题的程序使其显示每行的总和。

- 4. （练习）编写一个 C++ 程序，相加两个数组元素并显示结果：
| 第一个数组 | 第二个数组 |
| --- | --- |

- 5. （数据处理）编写一个 C++ 程序，找到二维数组中的最大值。
    b. 修改第 5 题的程序使其也显示行列索引。

- 6. （数据处理）编写一个 C++ 程序，按升序对二维数组进行排序。

- 7. （电气工程）一位工程师构建了一个3 行 5 列的二维数组。编写一个 C++ 程序交互式地输入电压并确定总和：
    - 使用什么方法可以每次初始化数组？
    - 如何修改你的 7a 程序以处理不存在电压的情况？也就是说，可以使用什么电压来指示无效电压，你的程序必须如何修改以排除此类电压？

## 413 数组

## 数组参数

数组元素传递函数的方式与标量变量相同；在调用函数时，它们作为订阅变量包含。例如，以下函数将 volts[2] 和 volts[6] 的值传递给 findMin()：

```cpp
findMin(int volts[2], int volts[6]);
```
