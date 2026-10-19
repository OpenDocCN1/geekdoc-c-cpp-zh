

要查看 sales 数组，请显示 QuickWatch 窗口（Debug, QuickWatch），在 Expressions 中输入 sales，点击 Add Watch，然后点击 Close。展开 sales 数组以查看值，显示如下：

| Name | Value |
|------|-------|
| sales | {string[10, 5]} |
| [0, 0] | "1033" |
| [0, 1] | "16" |
| [0, 2] | "32" |
| [0, 3] | "23" |
| [0, 4] | "40" |
| [1, 0] | null |
| [1, 1] | null |
| [1, 2] | null |

点击继续以监视 sales 数组第 1 行的值。
点击继续直到 Sales.txt 中的所有行都复制到数组中。

## Part 2

搜索 2-D 数组以查找指定产品号的销售额。这是在 btnDisplaySales 的 Click 事件处理程序中完成的。代码如 Figure 8-36 所示。

### Figure 8-36: Code to search the 2-D array

```
54
55 private void btnDisplaySales_Click(object sender, EventArgs e)
56 {
57     int row = 0, column, rowSum=0;
58     string fmtStr = "{0,-20}{1,8}";
59     lstDisplay.Items.Clear();
60     lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Total Sales"));
61
62     for (row = 0; row < recordCount; row++)
63         // recordCount is the number of rows with data in it
64     {
65         // Check whether column 0 of current row matches Product#
66         if (sales[row, 0] == txtProdNumber.Text)
67         {
68             // Add columns 1 - 4
69             rowSum = int.Parse(sales[row, 1]) + int.Parse(sales[row, 2]) +
70                     int.Parse(sales[row, 3]) + int.Parse(sales[row, 4]);
71             // Alternate method using a loop:
72             for (column = 1; column <= 4; column++)
73                 rowSum = rowSum + int.Parse(sales[row, column]);
74
75             lstDisplay.Items.Add(string.Format(fmtStr, txtProdNumber.Text, rowSum));
76             return;     // Exit the method, if a matching product is found
77         }
78     }
```

## Jagged Arrays

锯齿数组与二维数组类似，只是各行的长度可以不同。它是一个一维数组，其中每个元素都是一个大小不固定的数组。Figure 8-37 显示了一个具有三行的锯齿数组示例。

### Figure 8-37: Jagged array

Rows
0 0 1 2 3
0 16 32 23 40
1 144 182
2 54 49 72

这就是你创建具有三行的锯齿 int 类型数组的方式：

```
int[][] jaggedSales = new int[3][];
```

请注意，变量的声明包含两组方括号，表示它是一个数组的数组。此外，列数未指定。

你按如下方式为每一行指定列数和初始值（可选）：

```
jaggedSales[0] = new int[4] {16, 32, 23, 40};
jaggedSales[1] = new int[2] {144, 182};
jaggedSales[2] = new int[3] {54, 49, 72};
```

你通过指定行和列索引来访问数组的元素。例如，jaggedSales[2][1] 的值为 49。

## Review Question

8-11 以下代码创建了一个二维数组，然后在名为 lstDisplay 的 ListBox 中显示数组的一个元素。

```
int[,] sales = {{ 16, 32, 23, 40 }, { 144, 182, 1679, 205 }, { 54, 49, 72, 63 }};
lstDisplay.Items.Add(sales[1, 3]);
```

ListBox lstDisplay 中显示的输出会是什么？

## Programming Assignment 2

本练习的主要目标是让你获得以下方面的经验：

- 1. 设计和创建包含不同类型控件（如 RadioButtons 和 ComboBoxes）的用户界面
- 2. 从文本文件读取和写入文本文件
- 3. 使用数组

你需要开发第 3 章编程练习 1 中指定的系统的增强版本。“Ace Auto Rentals”是一家小型汽车租赁企业。Ace 希望你开发一个应用程序，让他们能够按如下方式处理租赁费用：

创建一个表单 EnterRentals，允许用户为每次汽车租赁执行以下操作：

- 1. 输入五位客户号、客户姓名、租赁日期和租赁天数。
- 2. 选择汽车类型。当前选项为

**SUV, minivan, luxury, full size, midsize and compact.**

此列表可能会更改。

为了让用户轻松选择汽车类型并查看每日租赁费率，首先你必须将每种汽车类型和对应的费率存储在名为 AutoTypes.txt 的文本文件中（SUV = $ 80, minivan = $70, luxury = $50, full size = $40, midsize = $35 and compact = $25）。

每次打开表单时，读取汽车类型和费率，并按汽车类型排序将汽车类型添加到 ComboBox 或 ListBox 中，以便用户可以从列表中选择一个。

此外，将汽车类型存储在名为 autoTypes 的数组中，并将费率存储在另一个名为 dailyRates 的数组中。

当用户选择一种汽车类型时，从数组中找到所选汽车类型的费率并在 Label 中显示费率。
- 3. 选择一个折扣类别。当前选项为

**Normal, State Employees, Business and Favorite Customer.**

此列表不太可能更改。

选择合适的 GUI 类型让用户选择一个类别。
- 4. 计算租赁费用、折扣和总成本。
  - 租赁费用：天数 x 每日租赁费率
  - 折扣：Normal = 0%，State emps = 15%，Business = 10%，Favorite = 20%
  - 总成本：租赁费用 + 折扣

- 5. 以适当的标签清晰地显示天数、租赁费用、折扣和总成本。

- 6. 将客户号、客户姓名、汽车类型、天数、租赁费用、折扣和总成本写入文本文件 Rental.txt。用户应能够清除数据并在无需退出并重新运行表单的情况下为其他客户输入租赁数据。

## Collections

集合与数组类似，可以保存一组元素（项目）。元素可以是任何数据类型，如简单数字、字符串、数组或对象。集合与数组有何不同？本章描述了集合的独特功能并介绍了其实际应用。

## Topics

| 9.1 Introduction to Collections | 9.3 Dictionary<TKey, TValue>Collection |
| 9.2 List<T>Collection |  |

### 9.1 Introduction to Collections

你在处理 ComboBox 和 ListBox 等 GUI 控件时已经使用过集合。要在这些控件中创建项目列表，你使用 Items.Add() 方法将项目添加到这些控件的 Items 集合中，而无需像 C# 数组那样指定元素的索引。集合提供了多种此类方法，使你无需了解底层结构即可轻松操作它们。此外，当你插入新项目时，集合的大小会自动增加。

.Net Framework 提供的用于创建集合的类可以大致分为泛型（类型化）和非泛型（未类型化）集合。泛型集合是强类型——也就是说，你可以指定可以存储在集合中的单一类型。非泛型集合允许在单个集合中存储不同类型的元素。这意味着一个本意为某种类型（如 float）的非泛型集合可能包含意外添加的字符串。因此，除非有特殊原因，否则通常不建议使用非泛型。两种类型的集合都可能包含字符串、数组、对象和值类型如 int 和 float。

一些泛型类型有对应的非泛型类型，而另一些则没有。表 9-1 显示了一些常用的泛型集合及其对应的非泛型集合（如果有）。

表 9-1 中列出的不同集合的附加功能包括以下内容：

- List 不需要唯一键，但 Dictionary、SortedList 和 SortedDictionary 需要唯一键。
- SortedList 和 SortedDictionary 保持数据按排序顺序，使插入和删除项目通常比未排序集合效率更低。

