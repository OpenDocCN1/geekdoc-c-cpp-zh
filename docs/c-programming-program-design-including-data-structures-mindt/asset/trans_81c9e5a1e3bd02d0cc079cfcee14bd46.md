
如果这样做，那么在一维数组中操作数据的算法就会有些复杂，因为必须知道一行在哪里结束、另一行从哪里开始。还必须正确计算特定元素的索引。C++ 通过使用二维数组简化了以表格形式操作数据的处理。本节首先讨论如何声明二维数组，然后介绍操作二维数组中数据的方法。

**二维数组：** 由固定数量的分量按行和列（即二维）排列而成的集合，其中所有分量都具有相同类型。

声明二维数组的语法是：

```cpp
dataType arrayName[intExp1][intExp2];
```

其中 `intExp1` 和 `intExp2` 是产生正整数值的常量表达式。这两个表达式 `intExp1` 和 `intExp2` 分别指定数组中的行数和列数。

语句：

```cpp
double sales[10][5];
```

声明了一个 10 行 5 列的二维数组 `sales`，其中每个分量的类型都是 `double`。与一维数组一样，行编号为 0……9，列编号为 0……4（见图 8-13）。

![](img/b217c421655b51e7494cf3b89bb5432d_611_0.png)

**图 8-13** 二维数组 sales

## 访问数组分量

要访问二维数组的分量，需要一对索引：一个用于行位置（在前），一个用于列位置（在后）。

访问二维数组分量的语法是：

```cpp
arrayName[indexExp1][indexExp2]
```

其中 `indexExp1` 和 `indexExp2` 是产生非负整数值的表达式。`indexExp1` 指定行位置，`indexExp2` 指定列位置。

语句：

```cpp
sales[5][3] = 25.75;
```

将 25.75 存入数组 `sales` 的第 5 行第 3 列（即第六行第四列）（见图 8-14）。

![](img/b217c421655b51e7494cf3b89bb5432d_612_0.png)

假设：

```cpp
int i = 5;
int j = 3;
```

那么，前面的语句：

```cpp
sales[5][3] = 25.75;
```

等价于：

```cpp
sales[i][j] = 25.75;
```

因此，索引也可以是变量。

## 声明时初始化二维数组

与一维数组一样，二维数组可以在声明时初始化。下面的例子有助于说明这一概念。考虑以下语句：

```cpp
int board[4][3] = {{2, 3, 1},
                   {15, 25, 13},
                   {20, 4, 7},
                   {11, 18, 14}};
```

该语句将 `board` 声明为一个 4 行 3 列的二维数组。第一行的元素分别是 2、3 和 1；第二行的元素分别是 15、25 和 13；第三行的元素分别是 20、4 和 7；第四行的元素分别是 11、18 和 14。图 8-15 展示了数组 `board`。

![](img/b217c421655b51e7494cf3b89bb5432d_613_0.png)

| board | [0] | [1] | [2] |
|---|---:|---:|---:|
| [0] | 2 | 3 | 1 |
| [1] | 15 | 25 | 13 |
| [2] | 20 | 4 | 7 |
| [3] | 11 | 18 | 14 |

**图 8-15** 二维数组 board

在声明二维数组时初始化它：

- 1. 每一行的元素都包含在一对花括号中，并用逗号分隔。
- 2. 所有行的集合包含在花括号中。
- 3. 对于数值数组，如果未指定某一行的所有分量，则未指定的分量会被初始化为 0。在这种情况下，必须至少给出一个值来初始化该行的所有分量。

## 二维数组与枚举类型

> **注意**  
> 理解本节需要先阅读第 7 章中的“枚举类型”一节。

也可以将枚举类型用于数组索引。考虑以下语句：

```cpp
const int NUMBER_OF_ROWS = 6;
const int NUMBER_OF_COLUMNS = 5;
enum carType {GM, FORD, TOYOTA, BMW, NISSAN, VOLVO};
enum colorType {RED, BROWN, BLACK, WHITE, GRAY};
int inStock[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];
```

这些语句定义了 **carType** 和 **colorType** 枚举类型，并将 **inStock** 定义为 6 行 5 列的二维数组。假设 **inStock** 中的每一行对应一种汽车类型，每一列对应一种颜色类型。也就是说，第一行对应汽车类型 **GM**，第二行对应汽车类型 **FORD**，依此类推。类似地，第一列对应颜色类型 **RED**，第二列对应颜色类型 **BROWN**，依此类推。进一步假设 **inStock** 中的每个条目表示特定类型和颜色的汽车数量（见图 8-16）。

![](img/b217c421655b51e7494cf3b89bb5432d_614_0.png)

**图 8-16** 二维数组 `inStock`

语句：

```cpp
inStock[1][3] = 15;
```

等价于以下语句（见图 8-17）：

```cpp
inStock[FORD][WHITE] = 15;
```

![](img/b217c421655b51e7494cf3b89bb5432d_614_1.png)

**图 8-17** `inStock[FORD][WHITE]`

第二条语句可以轻松传达信息——即，将 **WHITE FORD** 汽车的数量设置为 15。这个例子说明，枚举类型可以有效地用于使程序可读且易于管理。

## 处理二维数组

可以通过四种方式处理二维数组：

- 1. 处理单个元素。
- 2. 处理整个数组。
- 3. 处理数组的特定行，称为**行处理**。
- 4. 处理数组的特定列，称为**列处理**。

处理单个元素就像处理单个变量。初始化数组和打印数组是处理整个二维数组的示例。查找一行（列）中的最大元素或求一行（列）的和，是行（列）处理的示例。我们将在讨论中使用以下声明：

```cpp
const int NUMBER_OF_ROWS = 7;        //This can be set to any number.
const int NUMBER_OF_COLUMNS = 6;     //This can be set to any number.

int matrix[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];
int row;
int col;
int sum;
int largest;
int temp;
```

![](img/b217c421655b51e7494cf3b89bb5432d_615_0.png)

**图 8-18** 二维数组 *matrix*

二维数组的所有分量，无论是行还是列，类型都相同。如果单独看一行，可以看出它只是一个一维数组。单独看一列也是一个一维数组。因此，在处理二维数组的特定行或列时，我们使用与处理一维数组类似的算法。我们将借助前面声明的二维数组进一步解释这一概念。

假设要处理 `matrix` 的第 5 行（即 `matrix` 的第六行）。`matrix` 第 5 行的元素是：

`matrix[5][0]`、`matrix[5][1]`、`matrix[5][2]`、`matrix[5][3]`、`matrix[5][4]` 和 `matrix[5][5]`

可以看到，在这些分量中，第一个索引（行位置）固定为 5。第二个索引（列位置）的范围是 0 到 5。因此，可以使用以下 `for` 循环来处理第 5 行：

```cpp
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    process matrix[5][col]
```

显然，这个 `for` 循环等价于以下 `for` 循环：

```cpp
row = 5;
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    process matrix[row][col]
```

类似地，假设要处理 `matrix` 的第 2 列，即 `matrix` 的第三列。这一列的元素是：

`matrix[0][2]`、`matrix[1][2]`、`matrix[2][2]`、`matrix[3][2]`、`matrix[4][2]`、`matrix[5][2]` 和 `matrix[6][2]`

这里，第二个索引（即列位置）固定为 2。第一个索引（即行位置）的范围是 0 到 6。在这种情况下，可以使用以下 `for` 循环来处理 `matrix` 的第 2 列：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    process matrix[row][2]
```

显然，这个 `for` 循环等价于以下 `for` 循环：

```cpp
col = 2;
for (row = 0; row < NUMBER_OF_ROWS; row++)
    process matrix[row][col]
```

接下来，我们讨论具体的处理算法。

### 初始化

假设要将第 4 行（即第五行）初始化为 0。如前所述，以下 `for` 循环可以完成此操作：

```cpp
row = 4;
for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    matrix[row][col] = 0;
```

如果要将整个 `matrix` 初始化为 0，还可以将第一个索引（即行位置）放入循环中。通过使用以下嵌套的 `for` 循环，我们可以将 `matrix` 的每个分量初始化为 0：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        matrix[row][col] = 0;
```
