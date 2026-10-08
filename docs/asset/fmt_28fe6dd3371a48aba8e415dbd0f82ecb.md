
```cpp
double computeAverage(int a[ ], int numberUsed);
//返回数组 a 前 numberUsed 个
// 元素的平均值。该数组保持不变。

void showDifference(const int a[ ], int numberUsed)
{
    double average = computeAverage(a, numberUsed);
    cout << "Average of " << numberUsed << " numbers:\n";
    cout << "The numbers are:\n";
    for (int i = 0; i < numberUsed; i++)
        cout << a[i] << " differs from " << average << endl;
}
```

这段代码将生成错误信息或警告信息，因为函数没有更改参数。如果你对某一特定类型的某个数组参数使用了它，那么你应该对所有其他具有该类型且不被函数修改的数组参数都使用它。其理由是为了在函数调用中进行函数调用。考虑下面的 `showDifference` 的定义，它与定义中使用的函数声明一起给出：

```cpp
double computeAverage(int a[ ], int numberUsed);
```

## 返回数组的函数

函数不能像返回 `int` 或 `double` 那样返回数组。有一种方法可以大致等同于返回数组的函数：返回数组的指针。然而，我们还没有介绍指针。我们将在第 9 章讨论数组和指针时讨论返回数组的指针。在此之前，你没有方法编写一个返回数组的函数。

## 案例研究 生产图表

在这个案例研究中，我们在自顶层设计中使用数组。我们使用索引变量和整个数组作为子任务的参数。

### 问题定义

Apex 塑料勺子制造公司委托我们编写一个程序，显示其四个工厂在某一周的生产能力的条形图。工厂按部门分开产量，例如茶勺部门、汤部门、勺部门、鸡尾勺部门等。此外，每个工厂的部门数量不同。例如，只有一个工厂生产鸡尾勺。输入是给出该工厂每个部门产量的列表。

### 输入

四个编号从 1 到 4 的制造工厂。对于这四个工厂中的每一个，都会给出以下输入：该工厂每个部门产量的列表。列表以一个负数作为哨兵值结束。

## 7.2 函数中的数组

### 433

#### 输出

一个显示每个工厂总产量的柱状图。柱状图中的每个星号代表 1000 个单位。每个工厂的产量都会四舍五入到最接近的 1000 个。

#### 问题分析

我们将使用一个数组 `production`，它将存储四个工厂中每个工厂的总产量。数组索引均从 0 开始。但由于工厂的编号为 1 到 4，而不是 0 到 3，因此我们不会使用工厂编号作为数组索引。相反，我们将把第 $n$ 号工厂的总产量存放在索引变量 `production[n-1]` 中。第 1 号工厂的总产量将存储在 `production[0]` 中，第 2 号工厂的数据位于 `production[1]` 中，以此此类推。

由于输出是以千为单位的，程序将对数组元素的值进行缩放。如果第 3 号工厂的总产量为 4040 个，则 `production[2]` 的值最初被设置为 4040。这个 4040 的值将被缩放为 4，使得 `production[2]` 的值变为 4，并在图中输出四个星号来表示第 3 号工厂的产量。

我们程序的任务可以分为以下几个子任务：

- `inputData`：读取每个工厂的输入数据，并将索引变量 `production[plantNumber - 1]` 的值缩放为该工厂的总产量，其中 `plantNumber` 是工厂的编号。
- `scale`：对于每个 `plantNumber`，将索引变量 `production[plantNumber - 1]` 的值改为正确的星号数量。
- `graph`：输出柱状图。

整个 `production` 数组将作为执行这些子任务的函数的参数。按照数组参数的通常做法，这意味着我们必须有一个额外的形式参数来表示明数组的大小，而在本例中，该大小等同于工厂的数量。我们将使用一个定义常量来表示工厂数量，该常量将作为 `production` 数组的大小。我们程序的主体、执行子任务的函数声明以及工厂数量的定义常量，如显示 7.5 所示。注意，由于没有理由更改传递给函数 `graph` 的数组参数，我们通过添加 `const` 修饰符将数组参数变为常量。显示 7.5 中的内容是我们程序的大纲，如果它在一个单独的文件，可以对该文件进行编译，以便我们在定义与所示函数声明对应的函数之前检查是否存在任何语法错误。

在编译了显示 7.5 所示的文件后，我们就准备好设计三个子任务的函数实现了。对于每一个任务，我们都会设计一个算法，编写函数代码，并在设计下一个函数之前对函数进行测试。

### 子任务

#### 434 第 7 章 / 数组

#### inputData 的算法设计

`inputData` 函数的声明和函数体的描述性注释如显示 7.5 所示。如显示 7.5) 所示，当调用 `inputData` 时，形式数组参数 `a` 将被数组 `production` 替换，由于程序的最后部分即最后一个工厂编号与工厂数量相同，形式参数 `lastPlantNumber` 将被 `NUMBER_OF_PLANTS` 替换。`inputData` 的算法非常直观：

- 对于 `plantNumber` 等于 1、2 直到 `lastPlantNumber` 的每一个值，执行以下操作：
  - 读取编号为 `plantNumber` 的工厂的所有数据。
  - 对这些数字求和。
  - 将 `production[plantNumber - 1]` 设置为该总和。

#### inputData 的编码

`inputData` 函数的算法翻译为以下代码：

```cpp
//Uses iostream:
void inputData(int a [], int lastPlantNumber)
{
    using namespace std;
    for (int plantNumber = 1; plantNumber <= lastPlantNumber; plantNumber++)
    {
        // 读取数据、求和并存入 a[plantNumber-1]
    }
}
```

Instead, we will place the total production for plant number n the indexed variable `production[n-1]`. The total output for plant number 1 will be held in `production[0]`, the figures for plant 2 will be in `production[1]`, and so forth.
