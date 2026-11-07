

![](img/d68f6199646ca63591a6d8419e0ed4ba_450_0.png)

**图 9.33** 两个矩阵相乘

结果单元格中的每个元素是对应行与对应列乘积之和。

```text
A = a * g + b * k + c * o
B = a * h + b * l + c * p
...
H = d * j + e * n + f * r
```

## 代码

现在我们定义接口文件、实现文件和应用文件。

**接口文件** 程序 9.19 展示了接口文件。

### 程序 9.19 *Matrix* 类的接口文件

```cpp
/****************************************************************
 * The interface file for the Matrix class. The only private data
 * members are the sizes of the matrix and the pointer that
 * points to the matrix in the heap.
 * The constructor creates a matrix in the heap and the destructor
 * deletes the allocated memory in the heap.
 * The setup member function fills the matrices randomly.
 * We have addition, subtraction, multiplication, and print
 * member functions.
 ***************************************************************/
#include <iostream>
#ifndef MATRIX_H
#define MATRIX_H
#include <cmath>
#include <cstdlib>
#include <iomanip>
#include <cassert>
using namespace std;

// Matrix class definition
class Matrix
{
    private:
    24        int rowSize;
    25        int colSize;
    26        int** ptr;
    27    public:
    28        Matrix (int rowSize, int colSize);
    29        ~Matrix ();
    30        void setup ();
    31        void add (const Matrix& second, Matrix& result) const;
    32        void subtract (const Matrix& second, Matrix& result) const;
    33        void multiply (const Matrix& second, Matrix& result) const;
    34        void print () const;
    35    };
    36    #endif
```

**实现文件** 程序 9.20 展示了实现文件。注意，`setup` 成员函数会随机填充矩阵，但在实际情况下，我们可以从文件中读取这些值。

### 程序 9.20 *Matrix* 类的实现文件

```cpp
    1    /************************************************************
    2     * We have implemented all member functions declared in the
    3     * interface file.
    4     * The implementation follows the description of operations
    5     * discussed before.
    6     ************************************************************/
    7    #include "matrix.h"
    8
    9    // Constructor: creates a matrix in the heap
    10   Matrix::Matrix (int r, int c)
    11   : rowSize (r), colSize (c)
    12   {
    13       ptr = new int* [rowSize];
    14       for (int i = 0; i < rowSize; i++)
    15       {
    16           ptr[i] = new int [colSize];
    17       }
    18   }
    19   // Destructor: deletes memory locations in the heap
    20   Matrix::~Matrix ()
    21   {
    22       for (int i = 0; i < rowSize ; i++)
    23       {
    24           delete [] ptr[i];
    25       }
    26       delete [] ptr;
    27   }
    28   // The setup fills the cells with random values between 1 and 5.
    29   void Matrix::setup()
    30   {
    31       for (int i = 0; i < rowSize; i++)
    32       {
    33           for (int j = 0; j < colSize; j++)
    34           {
    35               ptr[i][j] = rand() % 5 + 1;
    36           }
    37       }
    38   }
    39   // The add function adds second to the host and creates result.
    40   void Matrix::add (const Matrix& second, Matrix& result) const
    41   {
    42       assert (second.rowSize == rowSize && second.colSize == colSize);
    43       assert (result.rowSize == rowSize && result.colSize == colSize);
    44
    45       for (int i = 0; i < rowSize; i++)
    46       {
    47           for (int j = 0; j < second.colSize; j++)
    48           {
    49               result.ptr[i][j] = ptr[i][j] + second.ptr[i][j];
    50           }
    51       }
    52   }
    53   // The subtract function subtracts second from host.
    54   void Matrix::subtract (const Matrix& second, Matrix& result) const
    55   {
    56       assert (second.rowSize == rowSize && second.colSize == colSize);
    57       assert (result.rowSize == rowSize && result.colSize == colSize);
    58       for (int i = 0; i < rowSize; i++)
    59       {
    60           for (int j = 0; j < second.colSize; j++)
    61           {
    62               result.ptr[i][j] = ptr[i][j] - second.ptr[i][j];
    63           }
    64       }
    65   }
    66   // The multiply function multiplies second by host.
    67   void Matrix::multiply (const Matrix& second, Matrix& result) const
    68   {
    assert (colSize == second.rowSize);
    assert (result.rowSize == rowSize);
    assert (result.colSize == second.colSize);
    for (int i = 0; i < rowSize; i++)
    {
        for (int j = 0; j < second.colSize; j++)
        {
            result.ptr[i][j] = 0;
            for (int k = 0; k < colSize; k++)
            {
                result.ptr[i][j] += ptr[i][k] * second.ptr[k][j];
            }
        }
    }
}

// The print function prints the values of cells.
void Matrix::print() const
{
    for (int i = 0; i < rowSize; i++)
    {
        for (int j = 0; j < colSize; j++)
        {
            cout << setw (5) << ptr[i][j];
        }
        cout << endl;
    }
    cout << endl;
}
```

**应用文件** 程序 9.21 展示了使用 *Matrix* 类的应用程序。

### 程序 9.21 测试 *Matrix* 类的应用程序

```cpp
/************************************************************
 * We create several matrix objects in the heap, and we apply *
 * some operations on them.                                  *
 ************************************************************/
#include "matrix.h"

int main ()
{
    // Instantiation and setup of matrix1
    cout << "matrix1" << endl;
11    Matrix matrix1 (3, 4);
12    matrix1.setup ();
13    matrix1.print();
14    // Instantiation and setup of matrix2
15    cout << "matrix2" << endl;
16    Matrix matrix2 (3, 4);
17    matrix2.setup ();
18    matrix2.print ();
19    // Instantiation and setup of matrix3
20    cout << "A new matrix3" << endl;
21    Matrix matrix3 (4, 2);
22    matrix3.setup ();
23    matrix3.print ();
24    // Adding matrix2 to matrix1 and printing the resulting matrix
25    cout << "Result of matrix1 + matrix2" << endl;
26    Matrix addResult (3, 4);
27    matrix1.add (matrix2, addResult);
28    addResult.print ();
29    // Subtracting matrix2 from matrix1 and printing the resulting matrix
30    cout << "Result of matrix1 - matrix2" << endl;
31    Matrix subResult (3, 4);
32    matrix1.subtract (matrix2, subResult);
33    subResult.print ();
34    // Multiplying matrix1 and matrix3 and printing the resulting matrix
35    cout << "Result of matrix1 * matrix3" << endl;
36    Matrix mulResult (3, 2);
37    matrix1.multiply (matrix3, mulResult);
38    mulResult.print();
39    return 0;
40 }
```

```text
Run:
matrix1
   3       2       3       1
   4       4       5       1
   4       1       1       5
matrix2
   4       3       1       3
   3       5       1       5
   4       5       1       4
matrix3
   4       1
   5       5
   3       4
   2       1
```

**matrix1 + matrix2 的结果**

|  |  |  |  |
|---:|---:|---:|---:|
| 7 | 5 | 4 | 4 |
| 7 | 9 | 6 | 6 |
| 8 | 6 | 2 | 9 |

**matrix1 − matrix2 的结果**

|  |  |  |  |
|---:|---:|---:|---:|
| −1 | −1 | 2 | −2 |
| 1 | −1 | 4 | −4 |
| 0 | −4 | 0 | 1 |

**matrix1 × matrix3 的结果**

|  |  |
|---:|---:|
| 33 | 26 |
| 53 | 45 |
| 34 | 18 |

## 关键术语

- 取地址运算符；指针算术
- & 符号；指针类型
- 代码内存；锯齿数组
- 悬空指针；引用类型
- 泛型指针；引用变量
- 全局对象；按指针返回
- 堆内存；按引用返回
- 间接运算符；按值返回
- 内存泄漏；静态内存
- 空指针；栈内存
- 按指针传递；静态对象
- 按引用传递

## 小结

引用类型是一种复合类型，它允许同一内存位置以不同名称使用。

指针类型是一种表示内存地址的复合类型。指针变量是包含地址的变量。

C++ 程序使用的内存由四个不同的区域组成：代码内存（存放程序）、静态内存（存放全局对象和静态对象）、栈内存（存放参数和局部对象）以及堆内存（存放运行时创建的对象）。

## 问题

**PR-1.** 给定以下代码行，说明将打印什么。

```cpp
int x = 10;
int& y = x;
cout << x << " " << y;
```

