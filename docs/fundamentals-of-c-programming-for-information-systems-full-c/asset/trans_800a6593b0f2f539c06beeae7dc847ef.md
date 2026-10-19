
## 创建数组的通用语法

创建数组的语句的通用语法如下：

```
Type[] VariableName = new Type(ArraySize)
```

其中，ArraySize 是数组的元素个数，Type 是要存储在数组中的数据类型，VariableName 是任意有效的变量名。

或者，你也可以使用两条不同的语句：

```
Type[] VariableName
```

```
VariableName = new Type(ArraySize)
```

## 教程 1：使用一维数组：测试分数应用程序

在本教程中，你将使用简单的一维数组。

步骤 1-1：从文件夹 Tutorial_Starts 打开项目 Ch7_Arrays。

步骤 1-2：打开如下所示的窗体 Array_1D_Intro。

![](img/143bad48262566137acc9c41f668a88f_226_0.png)

步骤 1-3：打开 btnDemo 的 Click 事件处理程序。

步骤 1-4：在 btnDemo 的 Click 事件处理程序中添加创建数组 testScores 的语句，如图 7-3 所示，并在右花括号处设置一个断点。

图 7-3：创建数组的代码

```
19    private void btnDemo_Click(object sender, EventArgs e)
20    {
21        // Create array testScore with default values:
22        int[] testScore = new int[10];
```

步骤 1-5：运行项目，并单击 Demo 按钮。

步骤 1-6：程序中断时，显示“局部变量”窗口（Debug, Windows, Locals）。展开 testScore 以显示数组中索引 0 到 9 对应的 10 个元素的值，如图 7-4 所示。

图 7-4：显示数组的“局部变量”窗口

![](img/143bad48262566137acc9c41f668a88f_227_0.png)

## 创建具有非零初始值的数组：数组初始化器

可以使用数组初始化器创建初始值不是默认零值的数组，初始化器是用花括号括起来的逗号分隔的值列表，例如：

```
int[] testScore = { 85, 92, 87, 67, 83, 91, 73, 98, 83, 84 };
```

这种创建数组的方式不需要关键字 new，也不需要 = 号右侧指定类型和数组大小。C# 编译器会根据列表中数据项的数量推断数组大小，并像使用关键字时一样创建数组。

或者，你也可以将其拆分为两条语句，如下所示：

```
int[] testScore;
testScore = { 85, 92, 87, 67, 83, 91, 73, 98, 83, 84 };
```

步骤 1-7：注释掉语句 int[] testScore = new int[10]，并添加一条使用数组初始化器而不是关键字 new 创建数组的语句，如图 7-5 所示。在事件处理程序的右花括号处设置一个断点。

图 7-5：使用数组初始化器

```
19   private void btnDemo_Click(object sender, EventArgs e)
20   {
21       // Create array testScore with default values:
22       // int[] testScore = new int[10];
23
24       // Create array testScore using array initializer
25       int[] testScore = { 85, 92, 87, 67, 83, 91, 73, 98, 83, 84 };
```

步骤 1-8：运行项目，并单击 Demo 按钮。

程序中断时，显示“局部变量”窗口（Debug, Windows, Locals）。展开 testScore 以显示数组的 10 个元素的值，如图 7-6 所示。

图 7-6：显示数组初始化器效果的“局部变量”窗口

![](img/143bad48262566137acc9c41f668a88f_228_0.png)

## 复习题

7.1 引用类型变量与值类型变量有何不同？

7.2 考虑以下在名为 lstDisplay 的 ListBox 中计算并显示总销售额的代码：

int sales=2, totalSales = 10;
totalSales = totalSales + sales;
sales = 3;
lstDisplay.Items.Add(totalSales);

ListBox 中显示的 totalSales 值是多少？

7.3 编写一条语句，创建一个最多可容纳二十个学生姓名的数组，该数组由名为 student 的变量引用。

7.4 编写一条语句，创建一个名为 student 的变量，该变量可以引用 string 类型数组。再编写第二条语句，创建一个最多可容纳二十个学生姓名的数组，该数组由 student 引用。

7.5 编写一条语句，创建一个由一周七天缩写名称组成的数组，该数组由名为 weekDay 的变量引用。

## 7.2 向数组元素赋值

数组初始化器是在创建数组时向数组元素赋值的简单方法。然而，在从文件或数据库等来源读取数据的应用程序中，通常是从数据源读取数据，然后使用循环将其赋值给数组元素，这一点将在后面讨论。

为了帮助理解这个概念，首先来看如何通过指定元素索引向数组的单个元素赋值。例如，下面的语句

```
testScore[2] = 99;
```

会将值 99 赋给数组 testScore 的第三个元素，以替换原来的值 87。

你也可以使用变量作为索引，例如：

```
int index = 2;
testScore[index] = 99;  // you may use any valid variable name to represent the index.
```

这种使用变量指定索引的方法会在循环中用于为数组的每个元素赋值。

步骤 1-9：将图 7-7 中的代码添加到 Click 事件处理程序中，将第三个测试分数改为 99，并将第一个测试分数改为 89。

图 7-7：更改数组元素的值

```
private void btnDemo_Click(object sender, EventArgs e)
{
    // Create array testScore with default values:
    // int[] testScore = new int[10];

    // Create array testScore using array initializer
    int[] testScore = { 85, 92, 87, 67, 83, 91, 73, 98, 83, 84 };

    // Change the first test score to 89, and the third test score to 99:
    testScore[0] = 89;
    testScore[2] = 99;
}
```

步骤 1-10：运行项目，并单击 Demo 按钮。

步骤 1-11：程序中断时，显示“局部变量”窗口（Debug, Windows, Locals）。展开 testScore 以显示数组的 10 个元素的值。数组更新后的值如图 7-8 所示。

图 7-9：显示 testScore 的一个元素

```
19    private void btnDemo_Click(object sender, EventArgs e)
20    {
21        // Create array testScore with default values:
22        // int[] testScore = new int[10];
23
24        // Create array testScore using array initializer
25        int[] testScore = { 85, 92, 87, 67, 83, 91, 73, 98, 83, 84 };
26
27        // Change the first test score to 89, and the third test Score to 99:
28        testScore[0] = 89;
29        testScore[2] = 99;
30
31        // Display 3rd element of the array
32        int index = 2;
33        lstDisplay.Items.Add(testScore[index]);
```

步骤 1-14：运行窗体以观察输出。你应该看到分数 87。

现在开始练习吧！完成练习 7-1。

## 使用 for 循环访问数组元素

接下来，我们将编写代码，在 ListBox lstDisplay 中显示数组的每个元素及其索引值，如图 7-10 所示。

图 7-10：使用 for 循环显示数组的每个元素

![](img/143bad48262566137acc9c41f668a88f_231_0.png)

我们使用 for 循环将元素索引的值从 0 改为 9。注意，索引的上限（9）等于数组大小（10）减 1。

## 7.4 使用 foreach 循环访问数组元素

作为使用 for 循环访问数组每个元素的替代方法，可以使用 foreach 循环。通常，使用 foreach 循环可以方便地访问任何集合中的单个项。下面是如何使用 foreach 循环显示每个测试分数：

```
foreach (int score in testScore)
    lstDisplay.Items.Add(score);
```

在每次迭代中，foreach 循环都会自动将数组中的下一个元素复制到迭代变量 score 中，从第一个元素开始。因此，第一次循环时，score 被赋值为第一个元素（89）并显示在 ListBox 中；第二次循环时，score 被赋值为第二个元素（92）；这个过程一直持续到所有分数都显示出来。

将 foreach 循环与前面介绍的 for 循环进行比较：

```
for (int index = 0; index <= testScore.Length-1; index = index + 1)
    lstDisplay.Items.Add(index + "    " + testScore[index]);
```

注意，使用 foreach 循环时，无需初始化循环变量、递增循环变量或指定上限，因为访问元素时不需要指定索引。由于 foreach 循环中没有使用循环变量，因此 foreach 循环的输出（如图 7-13 所示）不包含索引值。

图 7-13：使用 foreach 循环显示每个分数

![](img/143bad48262566137acc9c41f668a88f_234_0.png)

## for 与 foreach 的对比

与 foreach 循环相比，for 循环通常在处理元素时提供更大的灵活性。在 for 循环中，你还可以为数组元素赋值，并且可以方便地处理多个大小相同的数组。

如果应用程序只需要按顺序访问单个数组的元素而无需修改它们，那么这基本上就是个人偏好的问题。

现在，让我们修改 foreach 循环，如图 7-14 所示，计算总分，然后计算平均分。

