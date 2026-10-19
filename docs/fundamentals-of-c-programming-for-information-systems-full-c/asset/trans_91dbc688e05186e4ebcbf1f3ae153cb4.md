

## 图 7-14：使用 foreach 循环计算平均值

```
int totalScore = 0;
lstDisplay.Items.Add("Score");
foreach (int score in testScore)
{
    lstDisplay.Items.Add(score);
    totalScore = totalScore + score;
}
float averageScore = (float)totalScore / testScore.Length;
lstDisplay.Items.Add("Average: " + averageScore.ToString("N"));
```

## foreach 循环的通用语法

```
Foreach (Type VariableName in ArrayName)
{
    Statements
}
```

**步骤 1-22：** 注释掉使用 for 循环计算平均值的代码（图 7-12 中的第 31–41 行），并添加图 7-14 中的代码，该代码使用 foreach 循环。

**步骤 1-23：** 运行项目并测试代码。

## 数组名称应为单数还是复数？

数组的名称应为单数如 testScore 还是复数如 testScores？由于数组包含多个数据项，复数形式可能更直观。当你使用 foreach 循环访问数组的每个元素时，如以下代码所示，使用复数形式（testScores）表示数组，使用单数形式（testScore）表示表示单个分数的变量会很方便：

```
foreach (int testScore in testScores)
    lstDisplay.Items.Add(testScore);
```

然而，当你使用索引引用单个分数时，名词的单数形式更有意义。例如，testScore[1] 比 testScores[1] 更清晰地表示单个分数。此外，在数组的某些高级用法中，名词的单数形式更有意义。在本书中，我们同时使用这两种形式。

## 复习题

**7.10**  使用 **foreach** 循环将以下数组的所有元素显示到名为 lstDisplay 的 ListBox 中：

```
string[] weekDay = {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"};
```

## 7.5 复制数组

由于数组是引用类型，你不能通过将引用变量赋给另一个引用变量来创建数组的单独副本。例如，
int[] temp1 = testScore;
不会创建数组 testScore 的副本。相反，temp 和 testScore 将引用同一个数组，如图所示。

![](img/143bad48262566137acc9c41f668a88f_236_0.png)

也就是说，只有一个数组，但有两个变量引用它。这意味着如果你更改 testScore 的一个元素，实际上你也在更改 temp1 的该元素。

步骤：7-24：将以下代码添加到 Demo 按钮的 Click 事件处理程序末尾，并在第 56 行和 57 行插入断点：

```
53
54
55    // Assign testScore to another reference variable - doesn't copy the array
    int[] temp1 = testScore;
56    testScore[9] = 69;
57
```

步骤 1-25：运行项目。当程序在第 56 行中断（在 testScore[9] 改为 69 之前）时，在 Locals 窗口（Debug, Windows, Locals）中展开 testScore 和 temp，观察 temp 的值与 testScore 相同。

步骤 1-26：单击 Run 继续执行。当程序在第 57 行中断时，在 Locals 窗口（Debug, Windows, Locals）中展开 testScore 和 temp，观察 temp[9] 的值与 testScore[9] 相同，如图 7-15 所示，尽管看起来你只更改了 testScore 的值。

## 图 7-15：temp1 的值已更改

![](img/143bad48262566137acc9c41f668a88f_236_1.png)

你可以使用 temp1 或 testScore 更改数组的任何元素。例如，temp1[8] 将更改也被 testScore 引用的数组的第九个元素。

## 图 7-18：通过复制 testScore 创建的 temp2

testScore

![](img/143bad48262566137acc9c41f668a88f_238_0.png)

temp2

![](img/143bad48262566137acc9c41f668a88f_238_1.png)

例如，执行语句

```
testScore[9] = 99
```

会更改 testScore 的最后一个元素，但不会影响 temp2 或 temp3。

然而，temp1 被更改，因为 temp1 使用以下语句被赋予了对 testScore 的引用；因此，temp1 和 testScore 指向同一个数组：

```
int[] temp1 = testScore;
```

## 步骤 1-29：添加以下代码将 testScore 的最后一个元素更改为 99。

```
testScore[9] = 99;
```

## 步骤 1-30：运行项目。当程序在第 66 行中断时，显示 Locals 窗口并观察 testScore 和 temp1 的最后一个元素为 99，但 temp2 和 temp3 的最后一个元素未更改。

## 使用 for 循环复制数组

你也可以使用 for 循环将一个数组的元素复制到另一个数组。这里的代码将 testScore 的元素复制到名为 temp4 的数组：

```
int[] temp4 = new int[10]; // or, int[] temp4 = new int[testScore.Length]
for (int index = 0; index <= testScore.Length - 1; index = index + 1)
    temp4[index] = testScore[index];
```

这里，索引从 0 变到上界以访问每个元素。因此，循环内的语句等价于 10 个不同的语句：

```
temp4[0] = testScore[0];
temp4[1] = testScore[1];
temp4[2] = testScore[2];
etc.
```

## 7.6 在数组中查找值

一维数组可以方便地用于查找值，例如查找指定商品的价格或查找某人的电话号码。

考虑一个月份名称的字符串数组和另一个存储产品每月销售量的 int 数组，如图 7-19 所示。应注意，在实际应用中，此类数据通常从数据库表或文件中读取，而不是硬编码。

## 图 7-19：创建数组 months 和 unitsSold 的代码

```
string[] months = { "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" };

int[] unitsSold = { 572, 645, 693, 564, 580, 756, 960, 756, 663, 678, 745, 960 };
```

要查找指定月份的销售量，首先从 months 数组中找到该月份的索引。然后，找到 unitsSold 数组中该索引位置存储的数据项。此方法仅在 months 和 units sold 以相同顺序存储时有效（即，unitsSold 的第一个元素对应于 months 数组中的第一个月，unitsSold 中的第二个元素对应于 months 数组中的第二个元素，等等）。

例如，要查找三月的销售量，你找到 March 的索引，为 2，然后找到 unitsSold 数组中索引位置 2 的数据项，为 693。找到数组中特定数据项的索引的一种简便方法是使用 Array.IndexOf 方法。

## Array.IndexOf 方法

Array.IndexOf 方法返回一维数组中指定数据项的索引。

该方法具有以下语法

```
Array.IndexOf(ArrayName, SearchValue)
```

例如，

```
Array.IndexOf(months, "March")
```

ArrayName 是 1-D 数组的名称，SearchValue 是你在数组中尝试查找的值。该方法返回匹配指定值的第一个元素的索引。如果未找到值，该方法返回 -1。由于 months 和 units sold 以相同顺序存储，你可以使用月份的索引来查找 unitsSold。

## 教程 2：使用 1-D 数组查找销售量

本教程创建一个名为 LookUpUsingArray 的窗体，允许用户查找指定月份的销售情况，如图 7-20 所示。

图 7-20：LookUpUsingArray 窗体

![](img/143bad48262566137acc9c41f668a88f_241_0.png)

步骤 2-1：在项目 Ch7_Arrays 中打开名为 LookupUsingArray 的窗体。

打开代码窗口。第 19–21 行的两个语句在类级别创建两个数组 months 和 unitsSold，如图 7-21 所示。这些数组在类级别创建，而不是在 btnDisplayUnitsSold 的 Click 事件处理程序内，以便它们不必每次用户单击按钮查找销售时都重新创建。

步骤 2-2：将图 7-21 中第 22–37 行所示的代码添加到 btnDisplayUnitsSold 的 Click 事件处理程序，以显示指定月份的销售量。

图 7-21：查找销售量的代码

```
19  string[] months = { "January", "February", "March", "April", "May", "June", "July",
20                  "August", "September", "October", "November", "December" };
21  int[] unitsSold = { 572, 645, 693, 564, 580, 756, 859, 756, 663, 678, 745, 958 };
22
23  private void btnDisplayUnitsSold_Click(object sender, EventArgs e)
24  {
25      string monthName = txtMonthName.Text;
26      int monthIndex, unitsSoldInMonth;
27
28      // Find the index of the month. Use the index to find units sold
29      monthIndex = Array.IndexOf(months, monthName);
30      if (monthIndex >= 0)  // if month is not found, index would be -1
31          unitsSoldInMonth = unitsSold[monthIndex];  // find units sold
32      else
33      {
34          MessageBox.Show("Month not found");
35          return;
36      }
37      lblUnitsSold.Text = unitsSoldInMonth.ToString();
```

第 29 行使用前面描述的 Array.IndexOf 方法从 months 数组中找到指定月份的索引。

