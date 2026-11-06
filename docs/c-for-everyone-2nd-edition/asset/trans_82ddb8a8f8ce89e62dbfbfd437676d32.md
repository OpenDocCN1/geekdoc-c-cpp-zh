
我们需要确定行动方案：

-   找到最小值。
-   找到它的位置。
-   从数组中删除该位置。
-   计算总和。

这样可行吗？让我们继续看示例。

我们找到最小值为 4。线性查找告诉我们，值 4 出现在位置 5。

| [0] | [1] | [2] | [3] | [4] | [5] | [6] |
|---|---|---|---|---|---|---|
| 8 | 7 | 8.5 | 9.5 | 7 | **4** | 10 |

我们删除它：

| [0] | [1] | [2] | [3] | [4] | [5] |
|---|---|---|---|---|---|
| 8 | 7 | 8.5 | 9.5 | 7 | 10 |

最后，我们计算总和：8 + 7 + 8.5 + 9.5 + 7 + 10 = 50。

这个演练表明我们的策略有效。

我们能做得更好吗？先找到最小值，然后再遍历一遍数组来获取其位置，似乎有点低效。

我们可以调整查找最小值的算法，使其返回最小值的位置。下面是原始算法：

```
double smallest = values[0];
for (int i = 1; i < size of values; i++)
{
    if (values[i] < smallest)
    {
        smallest = values[i];
    }
}
```

当我们找到最小值时，我们还希望更新位置：

```
if (values[i] < smallest)
{
    smallest = values[i];
    smallest_position = i;
}
```

事实上，这样一来就再也没有必要跟踪最小值了。它其实就是 values[smallest_position]。基于这一认识，我们可以如下调整算法：

```
int smallest_position = 0;
for (int i = 1; i < size of values; i++)
{
    if (values[i] < values[smallest_position])
    {
        smallest_position = i;
    }
}
```

经过这样的调整，我们可以用以下策略解决我们的问题：

-   找到最小值的位置。
-   从数组中删除它。
-   计算总和。

在 271 页的 How To 6.1 中，我们根据这一策略开发了一个 C++ 程序。

你应该熟悉基本算法的实现，以便能够调整它们。

我们在上一节讨论了 `min_position` 的算法：

```cpp
/**
   Gets the position of the minimum value from an array.
   @param values a partially filled array
   @param size the number of elements in values
   @return the position of the smallest element in values
*/
int min_position(double values[], int size)
{
   int smallest_position = 0;
   for (int i = 1; i < size; i++)
   {
      if (values[i] < values[smallest_position])
      {
         smallest_position = i;
      }
   }
   return smallest_position;
}
```

其余辅助函数使用第 6.2 节中的算法。你可以在本书的配套代码中找到这些实现。

## 步骤 4 考虑所实现函数的边界条件

大多数操作数组的函数都有点复杂，你必须小心处理正常情况和异常情况。空数组会怎样？只包含一个元素的数组会怎样？找不到匹配项时会怎样？存在多个匹配项时又会怎样？考虑这些边界条件，并确保你的函数能正确工作。

下面是一个此类考虑的示例。我们怎么知道调用 `min_position` 函数时传入的数组大小至少为 1？（回想一下，必须至少有一个元素才能找到最小值。）该函数由 `final_score` 函数调用。然而，可以想象 `final_score` 函数可能会被传入空数组来调用。我们需要么加入一个测试，要么在函数注释中添加限制。我们将选择后者，并将 `min_position` 函数的 `values` 参数变量的注释改为

```cpp
@param values a partially filled array of size >= 1
```

考虑另一个潜在问题。如果存在多个匹配项会怎样？这意味着一个学生有不止一次测试成绩较低。`final_score` 函数只删除该低分出现的一次，这正是期望的行为。

## 步骤 5 组装并测试完整程序。

现在我们准备将各个函数组合成一个完整的程序。在此之前，请考虑一些测试用例及其预期输出：

| 测试用例 | 预期输出 | 注释 |
| :--- | :---: | :--- |
| 8 7 8.5 9.5 7 5 10 | 50 | 参见步骤 1。 |
| 8 7 7 9 | 24 | 只应删除低分的一个实例。 |
| 8 | 0 | 删除低分后，不再有剩余分数。 |
| （无输入） | **错误** | 这不是合法输入。 |

## 6.6 二维数组

经常会出现这样的情况：你想存储具有二维布局的值集合。这类数据集常见于金融和科学应用中。由行和列的值构成的排列称为*二维数组*，或*矩阵*。

让我们探讨如何存储图 11 所示的示例数据：2010 年冬奥会花样滑冰比赛的奖牌数。

![](img/23fb3582e93ebc95909e1de029c3d388_305_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_305_1.png)

| 国家 | 金牌 | 银牌 | 铜牌 |
|---|---:|---:|---:|
| 加拿大 | 1 | 0 | 1 |
| 中国 | 1 | 1 | 0 |
| 德国 | 0 | 0 | 1 |
| 韩国 | 1 | 0 | 0 |
| 日本 | 0 | 1 | 1 |
| 俄罗斯 | 0 | 1 | 1 |
| 美国 | 1 | 1 | 0 |

**图 11** 花样滑冰奖牌数

### 6.6.1 定义二维数组

C++ 使用带两个下标的数组来存储二维数组。例如，下面是一个具有 7 行 3 列的数组定义，适合存储我们的奖牌数数据：

```cpp
const int COUNTRIES = 7;
const int MEDALS = 3;
int counts[COUNTRIES][MEDALS];
```

你可以按行分组来初始化该数组，如下所示：

```cpp
int counts[COUNTRIES][MEDALS] =
{
    { 1, 0, 1 },
    { 1, 1, 0 },
    { 0, 0, 1 },
    { 1, 0, 0 },
    { 0, 1, 1 },
    { 0, 1, 1 },
    { 1, 1, 0 }
};
```

与一维数组一样，二维数组一旦定义，就不能更改其大小。

### 6.6.3 计算行和列的总和

一项常见任务是计算行总和或列总和。在我们的示例中，行总和给出了某个国家获得奖牌的总数。

找到正确的索引值有点棘手，快速画个草图是个好主意。要计算第 i 行的总和，我们需要访问以下元素：

![](img/23fb3582e93ebc95909e1de029c3d388_307_0.png)

如你所见，我们需要计算 counts[i][j] 的总和，其中 j 的范围从 0 到 MEDALS - 1。下面的循环计算总和：

```cpp
int total = 0;
for (int j = 0; j < MEDALS; j++)
{
    total = total + counts[i][j];
}
```

计算列总和类似。对 counts[i][j] 求和，其中 i 的范围从 0 到 COUNTRIES - 1。

![](img/23fb3582e93ebc95909e1de029c3d388_307_1.png)

```cpp
int total = 0;
for (int i = 0; i < COUNTRIES; i++)
{
    total = total + counts[i][j];
}
```

row_total 函数不需要知道数组的行数。如果需要行数，请将其作为变量传入，如下例所示：

```cpp
int column_total(int table[][COLUMNS], int rows, int column)
{
    int total = 0;
    for (int i = 0; i < rows; i++)
    {
        total = total + table[i][column];
    }
    return total;
}
```

下面的程序演示了如何使用二维数组。该程序会打印奖牌数和行总和。

### ch06/medals.cpp

```cpp
#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

const int COLUMNS = 3;

/**
   Computes the total of a row in a table.
   @param table a table with 3 columns
   @param row the row that needs to be totaled
   @return the sum of all elements in the given row
*/
double row_total(int table[][COLUMNS], int row)
{
   int total = 0;
   for (int j = 0; j < COLUMNS; j++)
   {
      total = total + table[row][j];
   }
   return total;
}

int main()
{
   const int COUNTRIES = 7;
   const int MEDALS = 3;

   string countries[] =
   {
      "Canada",
      "China",
      "Germany",
      "Korea",
      "Japan",
      "Russia",
      "United States"
   };

   int counts[COUNTRIES][MEDALS] =
   {
```
