
```cs
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Windows.Forms;

10 namespace Selection_Sort

public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }

    // SelectionSort 方法接收一个 int 数组作为参数。
    // 它使用选择排序算法对数组进行排序。
    private void SelectionSort(int[] iArray)
    {
        int minIndex; // 扫描区域内最小值的索引
        int minValue; // 扫描区域内的最小值

        // 外层循环遍历数组中的所有元素，
        // 除了最后一个。startScan 标记了
        // 扫描应该开始的位置
        for (int startScan = 0; startScan < iArray.Length - 1; startScan++)
        {
            // 假设扫描区域的第一个元素
            minIndex = startScan;
            minValue = iArray[startScan];
            // 从相同区域的第二个元素开始扫描数组，
            // 寻找最小值。
            for (int index = startScan + 1; index < iArray.Length; index++)
            {
                if (iArray[index] < minValue)
                {
                    minValue = iArray[index];
                    minIndex = index;
                }
            }
            // 将具有最小值的元素与扫描区域
            // 中的第一个元素交换。
            Swap(ref iArray[minIndex], ref iArray[startScan]);
        }
    }

    // Swap 方法通过引用接收两个整数，
    // 并交换它们的内容。
    private void Swap(ref int a, ref int b)
    {
        int temp = a;
        a = b;
        b = temp;
    }

    private void goButton_Click(object sender, EventArgs e)
    {
        // 创建数组。
        int[] numbers = { 5, 2, 9, 1, 6, 3 };
        // 显示数组。
        foreach (int value in numbers)
        {
            originalListBox.Items.Add(value);
        }
        // 排序数组。
        SelectionSort(numbers);
        // 显示数组。
        foreach (int value in numbers)
        {
            sortedListBox.Items.Add(value);
        }
    }

    private void exitButton_Click(object sender, EventArgs e)
    {
        // 关闭表单。
        this.Close();
    }
}
```

### 二分查找算法

之前我们讨论了顺序搜索，它通过循环遍历数组，从第一个元素开始。它将每个元素与要查找的值进行比较，直到找到该值或遇到数组末尾。如果查找的值不在数组中，算法将失败。

顺序搜索的优点是简单：易于理解和实现。此外，它不需要数组中的数据经过排序。然而，它的缺点是效率低。如果要搜索的数组包含 20000 个元素，算法必须查看所有的 20000 个元素才能找到一个值。

在平均情况下，在数组开头或结尾找到项的概率是相同的。通常，对于包含 n 个元素的数组，顺序搜索在 n/2 次尝试内定位项。如果数组有 50000 个元素，顺序搜索在通常情况下会进行 25000 次比较。最大比较次数总是 n。

当顺序搜索无法定位某个项时，它必须对数组中的每个元素进行比较。随着失败搜索尝试次数的增加，平均比较次数也随增加。虽然顺序搜索算法对于小数组是足够的，但如果速度很重要，就不应该在大数组上使用。

二分查找是一种聪明的算法，比顺序搜索高效得多。它的唯一要求是数组值必须按顺序排序。它不是从数组第一个元素开始搜索，而是从中间元素开始。如果该元素大于目标值，则搜索结束。否则，如果中间的值大于或小于要查找的值，那么目标值（如果在列表中）将在数组的前半部分被找到。

如果在中间元素没有找到目标值，则对可能包含该值的一半重复此过程。例如，如果要搜索的是数组的后半部分，算法将测试其中间元素。如果在那里没有找到目标值，范围将缩小到位于之前或之后的

# 数组与列表

该元素。此过程一直持续，直到搜索的值被找到，或者没有更多元素可以测试。

以下是对数组执行二分查找方法的伪代码：

```
Method BinarySearch(array, searchValue)

Set first to 0

Set last to the last subscript in the array

Set position to -1

Set found to false

While found is not true and first is less than or equal to last

Set middle to the subscript half way between array[first] and array[last]

If array[middle] equals searchValue

Set found to true

Set position to middle

Else If array[middle] is greater than searchValue

Set last to -1

Else

Set first to middle + 1

End If

While

Return position
```

该算法使用三个变量来标记数组中的位置：`first`、`last` 和 `middle`。`first` 和 `last` 变量标记了当前搜索的数组部分的边界。它们用数组第一个元素和最后一个元素的下标初始化。`first` 和 `last` 之间中间元素的下标被计算并存储在 `middle` 变量中。如果数组中间的元素不包含搜索值，则调整 `first` 或 `last` 变量，使得在下次迭代中只搜索数组的上半部分或下半部分。这使得每次循环未能找到搜索值时，搜索范围减半。

以下 C# 方法对整数数组执行二分查找。它查找数值 `value` 的出现。如果找到，则返回数组下标。否则，返回 -1，表示该值未出现在数组中。

```csharp
1 private int BinarySearch(int[] iArray, int value)
2 {
3 int first = 0; // 数组第一个元素
4 int last = iArray.Length - 1; // 数组最后一个元素
5 int middle; // 搜索的中点
6 bool found = false; // 搜索位置
7 // 标记
8
9 // 查找该值。
10 while (found && first <= last)
11 {
12
13 // 计算中间点。
14 middle = (first + last) / 2;
15
16 // 如果在中点找到了值...
17 if (iArray[middle] == value)
18 {
19 found = true;
20 position = middle;
21 }
```

```csharp
21 // else 如果值在下半部分...
22 else if (iArray[middle] > value)
23 {
24 last = middle - 1;
25 }
26 // else 如果值在上半部分...
27 else
28 {
29 first = middle + 1;
30 }
31 }
33 // 返回项目的位置，如果未找到
34 则返回 -1。
35 return position;
36 }
```

如果你想查看一个使用二分查找算法的完整应用程序，请查看 `Student Sample Programs` 中 `Chap07` 文件夹下的 `Binary Search` 项目。它从文件中加载名称列表到数组中，并执行二分查找以在数组中查找特定名称。

### 检查点 (Checkpoint)

- 14 什么是搜索算法？
- 15 排序算法的目的是？
- 16 二分查找算法的唯一要求是什么？

### 二维数组

> 概念：二维数组类似于将多个相同的数组组合在一起。它适用于存储多组数据。

你到目前为止学习的数组被称为一维数组。它们之所以被称为一维数组是因为它们只能包含一组数据。二维数组（也称为 2D 数组）可以包含多组数据。将二维数组想象成具有行和列元素，如图 37 所示。该图显示了一个具有三行四列的二维数组。注意，行编号为 0、1 和 2，列编号为 0、1、2 和 3。数组中总共有 12 个元素。

图 37 二维数组

| 列 0 | 列 1 | 列 2 | 列 3 |
|---|---|---|---|
|| 0 | | | | |
| 行 1 | | | | |
| 行 2 | | | | |

二维数组对于处理多组数据非常有用。例如，假设你正在为一位老师设计一个成绩平均分程序。该老师有六个学生，每个学生在学期内参加了五次考试。一种方法是为每个学生创建一个一维数组，每个学生一个。这些数组每个都将有五个元素，对应每场考试。然而，这种方法非常繁琐，因为你必须单独处理这些数组。更好的方法是使用一个具有六行（每个学生一个）和五列（每场考试一个）的二维数组，如图 38 所示。

图 38 六行五列的二维数组

| 包含考试 1 分数的列 | 包含考试 2 分数的列 | 包含考试 3 分数的列 | 包含考试 4 分数的列 | 包含考试 5 分数的列 |
|---|---|---|---|---|
| 行 0 | 列 1 | 列 2 | 列 3 | 列 4 |
| 行 1 | | | | | |
| 行 2 | | | | | |
| 行 3 | | | | | |
| 行 4 | | | | | |
| 行 5 | | | | | |

- 这一行用于学生 1。
- 这一行用于学生 2。
- 这一行用于学生 3。
- 这一行用于学生 4。
- 这一行用于学生 5。
- 这一行用于学生 6。

### 声明二维数组

要声明一个二维数组，需要两个声明符：第一个用于行数，第二个用于列数。这里是一个具有三行四列的二维数组声明示例：

```csharp
double scores = new double[3,4];
```

注意逗号出现在第一组括号内。这表示变量引用了一个二维数组。数字 3 和 4 是大小声明符。第一个声明符指定行数，第二个声明符指定列数。注意大小声明符之间用逗号分隔。对于一维数组，最好使用命名常量作为大小声明符。这里有一个示例：

```csharp
int ROWS = 3;
int COLS = 4;
int[,] scores = new int[ROWS,COLS];
```

在处理二维数组中的数据时，每个元素都有两个下标：一个用于行，一个用于列。在 `scores` 数组中，行 0 的元素引用方式如下：

```csharp
scores[0,0]
scores[0,1]
scores[0,2]
scores[0,3]
```

行 1 的元素引用方式如下：

```csharp
scores[1,0]
scores[1,1]
scores[1,2]
scores[1,3]
```

以及行 2 的元素引用方式如下：

```csharp
scores[2,0]
scores[2,1]
scores[2,2]
scores[2,3]
```

图 39 展示了带有每个元素下标的数组。

图 39 `scores` 数组中每个元素的下标

| | 列 0 | 列 1 | 列 2 | 列 3 |
|---|---|---|---|---|
| | | | | |
| | | | | |
| 行 1 | | | | |
| 行 2 | | | | |
| 行 3 | | | | |

### 访问二维数组中的元素

要访问二维数组中的元素，必须使用两个下标：一个用于行，一个用于列。例如，假设我们有如下声明，并程序处理 `values` 数组：

```csharp
int ROWS = 5;
int COLS = 10;
int[,] values = new int[ROWS,COLS];
```

以下语句将 95 赋值给 `values[2,1]`：

```csharp
values[2,1] = 95;
```

程序使用嵌套循环处理二维数组，例如，为 `values` 数组的每个元素一个随机数：

```csharp
// 创建 Random 对象。
Random rand = new Random();
// 创建一个二维数组。
int ROWS = 5;
int COLS = 10;
int[,] values = new int[ROWS,COLS];
// 填充数组。
for (int row = 0; row < ROWS; row++)
{
    for (int col = 0; col < COLS; col++)
    {
        values[row, col] = rand.Next(100);
    }
}
```

并且以下嵌套循环将 `values` 数组的所有元素显示在名为 `outputListBox` 的控件中：

```csharp
// 显示数组。
for (int row = 0; row < ROWS; row++)
{
    for (int col = 0; col < COLS; col++)
    {
        outputListBox.Items.Add(values[row, col].ToString());
    }
}
```

### 二维数组的隐式大小确定与初始化

与一维数组一样，你可以为二维数组提供初始化列表。记住，当你为数组提供初始化列表时，你不能提供上限下标。在初始化二维数组时，必须指示维度。以下是带有初始化列表的二维数组示例：

```csharp
int[,] values = { {1, 2, 3},
                 {4, 5, 6},
                 {7, 8, 9} };
```
