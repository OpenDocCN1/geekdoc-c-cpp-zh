
以下语句说明如何在程序执行期间使用 string 类型的变量读取输入/输出文件的名称，并打开这些文件：

```cpp
ifstream infile;
string fileName;

cout << "Enter the input file name: ";
cin >> fileName;

infile.open(fileName.c_str());    //open the input file
```

当然，还必须在程序中包含头文件 string。输出文件也有类似的约定。

## 并行数组

如果两个（或更多）数组的对应分量保存相关信息，则称这些数组为**并行**数组。

假设你需要记录学生的课程成绩及其学号，以便在学期末公布成绩。进一步假设一个班最多有 50 名学生，且他们的学号是 5 位数。因为可能有 50 名学生，所以需要 50 个变量来存储学生学号，以及 50 个变量来存储他们的成绩。你可以声明两个数组：int 类型的 studentId 和 char 类型的 courseGrade。每个数组有 50 个分量。此外，studentId[0] 和 courseGrade[0] 将存储第一个学生的学号和课程成绩，studentId[1] 和 courseGrade[1] 将存储第二个学生的学号和课程成绩，依此类推。

下列语句：

```cpp
int studentId[50];
char courseGrade[50];
```

声明了这两个数组。

假设需要将数据输入这些数组，而数据以如下形式提供在文件中：

```text
studentId courseGrade
```

例如，一个示例数据集为：

```text
23456 A
86723 B
22356 C
32733 B
11892 D
.
.
.
```

假设使用 ifstream 变量 infile 打开输入文件。因为每个数组的大小为 50，所以每个数组最多可以存储 50 个元素。此外，班里学生人数可能少于 50。因此，

## 访问数组分量

要访问二维数组的分量，需要一对下标：一个表示行位置，一个表示列位置。

访问二维数组分量的语法为：

```text
arrayName[indexExp1][indexExp2]
```

其中 `indexExp1` 和 `indexExp2` 是产生非负整数值的表达式。`indexExp1` 指定行位置；`indexExp2` 指定列位置。

下列语句：

```cpp
sales[5][3] = 25.75;
```

将 25.75 存储到数组 `sales` 的第 5 行第 3 列（即第六行第四列）中（见图 9-11）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_560_0.png)

图 9-11  `sales[5][3]`

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

因此，下标也可以是变量。

## 声明时初始化二维数组

与一维数组一样，二维数组可以在声明时初始化。下面的例子有助于说明这一概念。考虑下列语句：

```c
int board[4][3] = {{2, 3, 1},
                   {15, 25, 13},
                   {20, 4, 7},
                   {11, 18, 14}};
```

这条语句将 board 声明为一个四行三列的二维数组。第一行的分量是 2、3 和 1；第二行的分量是 15、25 和 13；第三行的分量是 20、4 和 7；第四行的分量分别是 11、18 和 14。图 9-12 显示了数组 board。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_561_0.png)

**图 9-12** 二维数组 board

在声明二维数组时初始化它：

- 1. 每一行的元素用花括号括起来，并用逗号分隔。
- 2. 所有行都用花括号括起来。
- 3. 对于数值数组，如果未指定某一行的所有分量，则未指定的分量初始化为 0。在这种情况下，必须至少给出一个值，才能初始化某一行的所有分量。

## 二维数组与枚举类型

> **注意** 理解本节需要先阅读第 8 章中的“枚举类型”一节。

也可以将枚举类型用于数组下标。考虑下列语句：

```c
const int NUMBER_OF_ROWS = 6;
const int NUMBER_OF_COLUMNS = 5;
enum carType {GM, FORD, TOYOTA, BMW, NISSAN, VOLVO};
enum colorType {RED, BROWN, BLACK, WHITE, GRAY};

int inStock[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];
```

这些语句定义了 `carType` 和 `colorType` 枚举类型，并将 `inStock` 定义为六行五列的二维数组。假设 `inStock` 中的每一行对应一种汽车类型，每一列对应一种颜色类型。也就是说，第一行对应汽车类型 `GM`，第二行对应汽车类型 `FORD`，依此类推。类似地，第一列对应颜色类型 `RED`，第二列对应颜色类型 `BROWN`，依此类推。进一步假设 `inStock` 中的每个条目表示某种类型和颜色的汽车数量（见图 9-13）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_562_0.png)

**图 9-13**  二维数组 `inStock`

下列语句：

```text
inStock[1][3] = 15;
```

等价于下列语句（见图 9-14）：

```text
inStock[FORD][WHITE] = 15;
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_562_1.png)

**图 9-14**  `inStock[FORD][WHITE]`

第二条语句可以很容易地传达信息——即把 WHITE FORD 汽车的数量设置为 15。这个例子说明，枚举类型可以有效地用于使程序具有可读性且易于管理。

## 处理二维数组

二维数组可以通过三种方式处理：

- 1. 处理整个数组。
- 2. 处理数组的特定行，称为**行处理**。
- 3. 处理数组的特定列，称为**列处理**。

初始化和打印数组是处理整个二维数组的例子。查找某行（列）中的最大元素或求某行（列）的和是行（列）处理的例子。在讨论中，我们将使用以下声明：

```cpp
const int NUMBER_OF_ROWS = 7;    //This can be set to any number.
const int NUMBER_OF_COLUMNS = 6; //This can be set to any number.

int matrix[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];
int row;
int col;
int sum;
int largest;
int temp;
```

图 9-15 显示了数组 matrix。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_563_0.png)

**图 9-15** 二维数组 `matrix`

由于二维数组的分量都具有相同类型，因此任意行或列的分量也具有相同类型。这意味着二维数组的每一行和每一列都是一个一维数组。因此，在处理二维数组的特定行或列时，我们使用

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        matrix[row][col] = 0;
```

### 打印

通过使用嵌套的 `for` 循环，可以输出 `matrix` 的分量。下面的嵌套 `for` 循环打印 `matrix` 的分量，每行一行：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
{
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        cout << setw(5) << matrix[row][col] << " ";

    cout << endl;
}
```

### 输入

下面的 `for` 循环将数据输入到 `matrix` 的第 4 行，即第五行：

```cpp
row = 4;

for (col = 0; col < NUMBER_OF_COLUMNS; col++)
    cin >> matrix[row][col];
```

和前面一样，通过将行号放入循环中，可以将数据输入到 `matrix` 的每个分量中。下面的 `for` 循环将数据输入到 `matrix` 的每个分量中：

```cpp
for (row = 0; row < NUMBER_OF_ROWS; row++)
    for (col = 0; col < NUMBER_OF_COLUMNS; col++)
        cin >> matrix[row][col];
```

### 按行求和

下面的 `for` 循环求 `matrix` 第 4 行的和；也就是说，它把第 4 行的各分量相加。

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
