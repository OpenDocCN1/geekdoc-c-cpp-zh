
例如，假设你执行一系列语句，然后询问用户是否要再次执行它们。do 语句很合适，因为你在决定是否重复之前先执行这些语句：

```cpp
char response;
do
{
    // A sequence of statements
    ...
    cout << "Do it again?";
    cin >> response;
} while ( (response == 'Y') || (response == 'y') );
```

## A.6 数组和向量

- 数组是一种存储相同类型数据的容器

数组是一种存储相同数据类型的数据项（或条目）的容器。数组的内存位置（或元素）是有序的。数组有第一个元素、第二个元素，以此类推，也有最后一个元素。也就是说，数组拥有有限数量的元素。因此，在编写程序并执行之前，你必须知道特定数组所需的最大元素数量。由于你可以直接且以任意顺序访问数组元素，因此数组是一种直接访问（或随机访问）数据结构。

- 你可以直接且以任意顺序访问数组元素

### A.6.1 一维数组

当你决定在程序中使用数组时，必须声明它，并在声明时指明其条目的数据类型及其大小。以下语句声明了一个名为 maxTemps 的一维数组，它包含给定一周的每日最高气温：

```cpp
const int DAYS_PER_WEEK = 7;
double maxTemps[DAYS_PER_WEEK];
```

方括号表示法 [] 将 maxTemps 声明为数组。该数组最多可包含七个浮点值。

- 使用索引指定数组中的特定元素

你可以使用一个表达式（称为索引或下标，并用方括号括起来）直接引用 maxTemps 中的任何浮点条目。在 C++ 中，数组索引必须是 0 到 size - 1 范围内的整数值，其中 size 是数组中的元素数量。maxTemps 的索引范围是 0 到 DAYS_PER_WEEK - 1。例如，该数组中的第五个元素是 maxTemps[4]。如果 k 是一个值为 4 的整数变量，则 maxTemps[k] 是数组中的第五个元素，maxTemps[k+1] 是第六个元素。此外，maxTemps[k++] 在给 k 加 1 之前访问 maxTemps[k]。请注意，引用一维数组中的元素时使用一个索引。

- 数组索引的整数值大于或等于 0

图 A-6 说明了数组 maxTemps，它目前只包含五个温度值。数组中的最后一个值在 maxTemps[4] 中；maxTemps[5] 和 maxTemps[6] 的值未初始化，因此未知。

你可以使用枚举常量作为索引，因为它们具有整数值。例如，请考虑以下定义：

- 可以将枚举常量用作数组索引

```cpp
enum Day {SUN, MON, TUE, WED, THU, FRI, SAT};
```

根据此定义，maxTemps[THU] 与 maxTemps[4] 具有相同的含义。你也可以在处理数组的循环中使用枚举常量，如以下 for 语句所示：

```cpp
for (Day dayIndex = SUN; dayIndex <= SAT; dayIndex++)
    cout << maxTemps[dayIndex] << endl;
```

### 图 A-6 最多包含七个元素的一维数组

![](img/288a0c22d14d2450c1e772f228f867b0_731_0.png)

显然，在访问数组元素之前，必须为其赋值。你必须使用之前描述的索引表示法一次为一个数组元素赋值。请注意，如果 a 和 b 是相同类型的数组，则赋值 a = b 是非法的。

maxTemps 的数据类型是派生类型，即通过使用声明运算符（如 []）从基本类型派生出来的类型。使用 typedef 为派生类型命名通常很有用。因此，你可以编写：

```cpp
const int DAYS_PER_WEEK = 7;
typedef double ArrayType[DAYS_PER_WEEK];
ArrayType maxTemps;
```

并使 ArrayType 在整个程序中可用。

**初始化。** 你可以在首次声明数组时初始化其元素。例如，

> 你可以在声明数组时初始化它

```cpp
double maxTemps[DAYS_PER_WEEK] = {82.0, 71.5, 61.8, 75.0, 88.3};
```

该语句将 maxTemps 的前五个元素初始化为列出的值，并将最后两个元素初始化为零。

**将数组传递给函数。** 如果你想要一个计算一维数组中前 n 个元素平均值的函数，可以这样声明该函数：

```cpp
double getAverageTemp(double temperatures[], int n);
```

因为编译器不知道数组能容纳多少个项目，你还必须将数组的大小或要处理的数组项目数量传递给函数。传统上，数组作为第一个参数列出，项目数量作为第二个参数。例如，你可以这样调用该函数：

```cpp
double avg = getAverageTemp(maxTemps, 5);
```

其中 maxTemps 是之前定义的数组。

> 数组始终按引用传递给函数

无论你如何编写其参数，数组都不会按值传递给函数。数组始终按引用传递。此限制避免了可能复制许多数组条目的情况。因此，函数 getAverageTemp 可以修改 maxTemps 的元素，即使该数组是函数的输入。为防止此类更改，你可以通过在类型前加上 const 来将数组参数指定为常量引用参数，如下所示：

```cpp
double getAverageTemp(const double temperatures[], int n);
```

### 图 A-7 二维数组

![](img/288a0c22d14d2450c1e772f228f867b0_732_0.png)

### A.6.2 多维数组

你可以使用具有一个索引的一维数组来存储简单的数据集合。例如，你可以将 52 个温度值线性地一个接一个地排列。这些温度的一维数组可以表示这种组织方式。

- 数组可以有多个维度

你也可以声明多维数组。你使用多个索引来指定多维数组中的元素。假设你想要表示 52 周内每天的最低温度。以下语句声明了一个名为 minTemps 的二维数组：

```cpp
const int DAYS_PER_WEEK = 7;
const int WEEKS_PER_YEAR = 52;
double minTemps[DAYS_PER_WEEK][WEEKS_PER_YEAR];
```

这些语句指定了两个索引的范围：第一个索引范围是 0 到 6，而第二个索引范围是 0 到 51。大多数人将二维数组视为图 A-7 所示的矩形排列（或矩阵），形成行和列。ArrayType 定义中给出的第一个维度是行数。因此，minTemps 有 7 行和 52 列。该矩阵中的每一列都表示特定一周的七个每日最低温度。

要引用二维数组中的元素，必须指示包含该元素的行和列。你通过编写两个索引（每个都用方括号括起来）来指示行和列。例如，minTemps[1][51] 是第 2 行和第 52 列中的元素。在温度示例的上下文中，该元素包含第 52 周第 2 天（星期一）记录的最低温度。一维数组索引的规则也适用于多维数组的索引。

- 在二维数组中，第一个索引表示行，第二个索引表示列

作为在程序中使用二维数组的示例，请考虑以下程序片段，它确定先前描述的数组 minTemps 中的最小值。我们使用枚举常量来引用一周中的天数。

```cpp
enum Day {SUN, MON, TUES, WED, THURS, FRI, SAT};

// Initially, assume the lowest temperature is first in the array
double LowestTemp = minTemps[0][0];
Day dayOfWeek = SUN;
int weekOfYear = 1;

// Search array for lowest temperature
for (int weekIndex = 0; weekIndex < WEEKS_PER_YEAR; weekIndex++)
{
    for (Day dayIndex = SUN; dayIndex <= SAT; dayIndex++)
    {
        if (LowestTemp > minTemps[dayIndex][weekIndex])
        {
            LowestTemp = minTemps[dayIndex][weekIndex];
            dayOfWeek = dayIndex;
            weekOfYear = weekIndex + 1;
        } // end if
    } // end for
} // end for

// At this point, LowestTemp is the smallest value in minTemps and
// occurs on the day and week given by dayOfWeek and weekOfYear,
// that is, LowestTemp == minTemps[dayOfWeek][weekOfYear - 1].
```

虽然你可以声明超过两个维度的数组，但通常超过三个维度是不寻常的。然而，处理此类数组的技术与处理二维数组的技术类似。

**编程提示：** 引用多维数组元素时，不要使用逗号分隔的索引。例如，myArray[3,6] 不引用数组元素 myArray[3][6]。表达式 3,6 是一个逗号表达式，其值为列出的最后一项，即 6。因此，虽然 myArray[3,6] 是合法的，但其含义是 myArray[6]，它引用元素 myArray[0][6]。

**初始化。** 你可以像初始化一维数组一样初始化二维数组的元素。你按行列出初始值。例如，语句

```cpp
int x[2][3] = { { 1, 2, 3 },
             { 4, 5, 6 } }; // 2 rows, 3 columns
```

该语句初始化二维数组 x，使其显示为

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |

也就是说，这些语句按顺序初始化元素 x[0][0]、x[0][1]、x[0][2]、x[1][0]、x[1][1] 和 x[1][2]。通常，当你为多维数组赋予初始值时，最后一个（或最右侧）索引增加得最快。

### A.6.3 向量

另一种可以存储相同类型数据项的容器是 **向量**。向量类似于一维数组，但向量为程序员提供了简单数组中没有的其他功能。向量是名为 vector 的标准 C++ 类的一个对象。这个类是
