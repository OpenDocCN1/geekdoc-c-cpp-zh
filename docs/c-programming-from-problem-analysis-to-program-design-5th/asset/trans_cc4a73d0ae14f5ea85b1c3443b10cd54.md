

### 按列求和

与按行求和的情况类似，下面的嵌套 `for` 循环用于计算每一列的和：

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

### 每行和每列中的最大元素

如前所述，二维数组的另外两种操作是找出每行和每列中的最大元素，以及计算两条对角线的和。接下来，我们给出执行这些操作的 C++ 代码。

下面的 `for` 循环确定第 4 行中的最大元素：

```cpp
row = 4;
largest = matrix[row][0]; //Assume that the first element of
                          //the row is the largest.
for (col = 1; col < NUMBER_OF_COLUMNS; col++)
    if (largest < matrix[row][col])
        largest = matrix[row][col];
```

下面的 C++ 代码确定每行和每列中的最大元素：

```cpp
//Largest element in each row
for (row = 0; row < NUMBER_OF_ROWS; row++)
{
    largest = matrix[row][0]; //Assume that the first element
                              //of the row is the largest.
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

### 将二维数组作为参数传递给函数

二维数组可以作为参数传递给函数，并且它们是按引用传递的。基地址（即实际参数的第一个分量的地址）被传递给形式参数。如果 `matrix` 是二维数组的名称，那么 `matrix[0][0]` 就是 `matrix` 的第一个分量。

在计算机内存中存储二维数组时，C++ 使用**行序形式**。也就是说，先存储第一行，然后是第二行，接着是第三行，依此类推。

对于一维数组，在将其声明为形式参数时，我们通常省略数组的大小。由于 C++ 以行序形式存储二维数组，为了正确计算某个分量的地址，编译器必须知道一行在哪里结束、下一行从哪里开始。因此，在将二维数组声明为形式参数时，可以省略第一维的大小，但不能省略第二维；也就是说，必须指定列数。

假设我们有如下声明：

```cpp
const int NUMBER_OF_ROWS = 6;
const int NUMBER_OF_COLUMNS = 5;
```

考虑下面定义的函数 `printMatrix`：

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

该函数将行数未指定、列为五列的二维数组作为参数，并输出该二维数组的内容。在函数调用期间，实际参数的列数必须与形式参数的列数匹配。

类似地，下面的函数输出元素类型为 `int` 的二维数组中每一行元素的和。

```cpp
void sumRows(int matrix[][NUMBER_OF_COLUMNS], int noOfRows)
{
    int row, col;
    int sum;

    //Sum of each individual row
    for (row = 0; row < noOfRows; row++)
```

```cpp
void printMatrix(int matrix[][NUMBER_OF_COLUMNS],
                 int noOfRows);
void sumRows(int matrix[][NUMBER_OF_COLUMNS],
             int noOfRows);
void largestInRows(int matrix[][NUMBER_OF_COLUMNS],
                   int noOfRows);

int main()
{
    int board[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS]
        = {{23, 5, 6, 15, 18},
           {4, 16, 24, 67, 10},
           {12, 54, 23, 76, 11},
           {1, 12, 34, 22, 8},
           {81, 54, 32, 67, 33},
           {12, 34, 76, 78, 9}};    //Line 1

    printMatrix(board, NUMBER_OF_ROWS);    //Line 2
    cout << endl;                          //Line 3
    sumRows(board, NUMBER_OF_ROWS);        //Line 4
    cout << endl;                          //Line 5
    largestInRows(board, NUMBER_OF_ROWS);  //Line 6

    return 0;
}

//Place the definitions of the functions printMatrix,
//sumRows, and largestInRows as described previously here.
```

### 示例运行：

```text
        23     5     6    15    18
         4    16    24    67    10
        12    54    23    76    11
         1    12    34    22     8
        81    54    32    67    33
        12    34    76    78     9

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

在该程序中，第 1 行的语句声明并初始化 `board` 为一个六行五列的二维数组。第 2 行的语句使用函数 `printMatrix` 输出 `board` 的元素（参见示例运行的前六行）。第 4 行的语句使用函数 `sumRows` 计算并打印每一行的和。第 6 行的语句使用函数 `largestInRows` 查找并打印每一行中的最大元素。

### 字符串数组

假设你需要执行一项操作，例如按字母顺序排列一组姓名。由于每个姓名都是一个字符串，存储这组姓名的一种便捷方式是使用数组。在 C++ 中，可以使用数据类型 `string` 或字符数组（C 字符串）来操作字符串。此外，在某些编译器上，数据类型 `string` 在标准 C++（即非 ANSI/ISO 标准 C++）中可能不可用。本节将说明操作字符串列表的两种方式。

### 字符串数组与 `string` 类型

使用数据类型 `string` 处理字符串列表非常简单。假设列表最多包含 100 个姓名。你可以声明一个包含 100 个 `string` 类型分量的数组，如下所示：

```cpp
string list[100];
```

诸如赋值、比较和输入/输出等基本操作都可以对 `string` 类型的值执行。因此，可以像处理本章第一部分讨论的任何一维数组一样处理 `list` 中的数据。

### 字符串数组与 C 字符串（字符数组）

假设列表中最大的字符串（例如，姓名）长度为 15 个字符，并且列表中有 100 个字符串。你可以声明一个 100 行、16 列的字符二维数组，如下所示（参见图 9-16）：

```cpp
char list[100][16];
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_570_0.png)

**图 9-16** 字符串数组 `list`

现在，对于每个 `j`（0 <= j <= 99），`list[j]` 是一个长度至多为 15 个字符的字符串。下面的语句将 `"Snow White"` 存储到 `list[1]` 中（参见图 9-17）：

```cpp
strcpy(list[1], "Snow White");
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_571_0.png)

**图 9-17** 数组 `list`，显示 `list[1]`

假设你想读取数据并存储到 `list` 中，并且每行一个条目。下面的 `for` 循环可以完成此任务：

```cpp
for (j = 0; j < 100; j++)
    cin.get(list[j], 16);
```

下面的 `for` 循环输出每一行中的字符串：

```cpp
for (j = 0; j < 100; j++)
    cout << list[j] << endl;
```

你还可以使用其他字符串函数（如 `strcmp` 和 `strlen`）以及 `for` 循环来操作列表。

> **注意：** 数据类型 `string` 定义了赋值、连接和关系运算等操作。如果你使用标准 C++ 头文件，并且你的编译器支持数据类型 `string`，我们建议你使用数据类型 `string` 来操作字符串列表。

### 声明二维数组的另一种方式

> **注意：** 可以跳过本节，不会影响内容的连贯性。

