
```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        matrix[row][col] = 0;
```

## 打印

通过使用嵌套 for 循环，可以输出 matrix 的各个分量。下面的嵌套 for 循环打印 matrix 的各个分量，每行输出一行：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
{
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        cout << setw(5) << matrix[row][col] << " ";

    cout << endl;
}
```

## 输入

下面的 for 循环将数据输入到第 4 行，即 matrix 的第 5 行：

```cpp
row = 4;

for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    cin >> matrix[row][col];
```

和之前一样，通过将行号放入循环中，可以将数据输入到 matrix 的每个分量中。下面的 for 循环将数据输入到 matrix 的每个分量中：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        cin >> matrix[row][col];
```

## 按行求和

下面的 for 循环求 matrix 第 4 行的和；也就是说，它将第 4 行的各个分量相加。

```cpp
sum = 0;
row = 4;
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    sum = sum + matrix[row][col];
```

再一次，通过将行号放入循环中，我们可以分别求出每一行的和。下面是求每一行各自之和的 C++ 代码：

```cpp
//Sum of each individual row
for (row = 0; row < NUMBER_OF_ROWS; row++)
{
    sum = 0;
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        sum = sum + matrix[row][col];

    cout << "Sum of row " << row + 1 << " = " << sum << endl;
}
```

## 按列求和

与按行求和的情况一样，下面的嵌套 `for` 循环求每一列各自的和：

```cpp
//Sum of each individual column
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
{
    sum = 0;
    for (row = 0; row < NUMBER_OF_ROWS; row++)
        sum = sum + matrix[row][col];

    cout << "Sum of column " << col + 1 << " = " << sum
         << endl;
}
```

## 每行和每列中的最大元素

如前所述，对二维数组的另外两种操作是求每一行和每一列中的最大元素，以及求两条对角线之和。接下来，我们给出执行这些操作的 C++ 代码。

下面的 `for` 循环确定第 4 行中的最大元素：

```cpp
row = 4;
largest = matrix[row][0]; //Assume that the first element of
                           // the row is the largest.

for (col = 1; col < NUMBER_OF_COLUMNS; col++)
    if (largest < matrix[row][col])
        largest = matrix[row][col];
```

下面的 C++ 代码确定每一行和每一列中的最大元素：

```cpp
//Largest element in each row
for (row = 0; row < NUMBER_OF_ROWS; row++)
{
    largest = matrix[row][0]; //Assume that the first element
                               //Of the row is the largest.
    for (col = 1; col < NUMBER_OF_COLUMNS; col++)
        if (largest < matrix[row][col])
            largest = matrix[row][col];

    cout << "The largest element in row " << row + 1 << " = "
         << largest << endl;
}

//Largest element in each column
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
{
    largest = matrix[0][col]; //Assume that the first element
                               //of the column is the largest.
    for (row = 1; row < NUMBER_OF_ROWS; row++)
        if (largest < matrix[row][col])
            largest = matrix[row][col];

    cout << "The largest element in column " << col + 1
         << " = " << largest << endl;
}
```

## 将二维数组作为参数传递给函数

二维数组可以作为参数传递给函数，并且按引用传递。基地址（即实际参数第一个分量的地址）被传递给形式参数。如果 **matrix** 是二维数组的名称，那么 `matrix[0][0]` 是 matrix 的第一个分量。

当将二维数组存储在计算机内存中时，C++ 使用**行序形式**。也就是说，先存储第一行，接着存储第二行，接着存储第三行，依此类推。

对于一维数组，当将其声明为形式参数时，我们通常省略数组的大小。由于 C++ 以行序形式存储二维数组，为了正确计算某个分量的地址，编译器必须知道一行在哪里结束、下一行在哪里开始。因此，当将二维数组声明为形式参数时，可以省略第一维的大小，但不能省略第二维；也就是说，必须指定列数。

假设有如下声明：

```cpp
const int NUMBER_OF_ROWS = 6;
const int NUMBER_OF_COLUMNS = 5;
```

考虑以下函数 printMatrix 的定义：

```cpp
void printMatrix(int matrix[][NUMBER_OF_COLUMNS],
                 int noOfRows)
{
    int row, col;

    for (row = 0; row < noOfRows; row++)
    {
        for (col = 0; col < NUMBER_OF_COLUMNS; col++)
            cout << setw(5) << matrix[row][col] << " ";

        cout << endl;
    }
}
```

该函数以一个行数未指定、列数为 5 的二维数组作为参数，并输出该二维数组的内容。在函数调用期间，实际参数的列数必须与形式参数的列数匹配。

类似地，下面的函数输出一个二维数组中每一行元素的和，该二维数组的元素类型为 `int`。

```cpp
void sumRows(int matrix[][NUMBER_OF_COLUMNS], int noOfRows)
{
    int row, col;
    int sum;

    //Sum of each individual row
    for (row = 0; row < noOfRows; row++)
    {
        sum = 0;

        for (col = 0; col < NUMBER_OF_COLUMNS; col++)
            sum = sum + matrix[row][col];

        cout << "Sum of row " << (row + 1) << " = " << sum
             << endl;
    }
}
```

![](img/f97f778697507bb6fdd80c5991210cba_568_0.png)

下面的函数确定每一行中的最大元素：

```cpp
void largestInRows(int matrix[][NUMBER_OF_COLUMNS],
                   int noOfRows)
{
    int row, col;
    int largest;

    for (row = 0; row < noOfRows; row++)
    {
        largest = matrix[row][0]; //Assume that the first element
                                  //of the row is the largest.
        for (col = 1; col < NUMBER_OF_COLUMNS; col++)
            if (largest < matrix[row][col])
                largest = matrix[row][col];

        cout << "The largest element of row " << (row + 1)
             << " = " << largest << endl;
    }
}
```

同样，你可以编写函数来求每一列元素的和、将数据读入二维数组、求每一行或每一列中的最大和/或最小元素，等等。

示例 9-10 展示了函数 printMatrix、sumRows 和 largestInRows 如何在程序中使用。

### 示例 9-10

下面的程序说明如何将二维数组作为参数传递给函数。

```cpp
// Two-dimensional arrays as parameters to functions.

#include <iostream>
#include <iomanip>

using namespace std;

const int NUMBER_OF_ROWS = 6;
const int NUMBER_OF_COLUMNS = 5;

void printMatrix(int matrix[][NUMBER_OF_COLUMNS],
                 int NUMBER_OF_ROWS);
void sumRows(int matrix[][NUMBER_OF_COLUMNS],
             int NUMBER_OF_ROWS);
void largestInRows(int matrix[][NUMBER_OF_COLUMNS],
                   int NUMBER_OF_ROWS);

int main()
{
    int board[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS]
                    = {{23, 5, 6, 15, 18},
                       {4, 16, 24, 67, 10},
                       {12, 54, 23, 76, 11},
                       {1, 12, 34, 22, 8},
                       {81, 54, 32, 67, 33},
                       {12, 34, 76, 78, 9}};    //Line 1

    printMatrix(board, NUMBER_OF_ROWS);           //Line 2
    cout << endl;                                  //Line 3
    sumRows(board, NUMBER_OF_ROWS);                //Line 4
    cout << endl;                                  //Line 5
    largestInRows(board, NUMBER_OF_ROWS);         //Line 6

    return 0;
}

//Place the definitions of the functions printMatrix,
//sumRows, and largestInRows as described previously here.
```

### 示例运行

```text
23      5       6      15      18
 4     16      24      67      10
12     54      23      76      11
 1     12      34      22       8
81     54      32      67      33
12     34      76      78       9

Sum of row 1 = 67
Sum of row 2 = 121
Sum of row 3 = 176
Sum of row 4 = 77
Sum of row 5 = 267
Sum of row 6 = 209

The largest element in row 1 = 23
The largest element in row 2 = 67
The largest element in row 3 = 76
The largest element in row 4 = 34
The largest element in row 5 = 81
The largest element in row 6 = 78
```

在这个程序中，第 1 行的语句声明并将 board 初始化为一个六行五列的二维数组。第 2 行的语句使用
