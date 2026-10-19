

## 表 9-1：常用集合

| Generic (typed) collections | Corresponding nongeneric (untyped) collections | Implementation and other features |
|---|---|---|
| List<T> T represents the type | ArrayList | Implemented as an array; allows accessing items by index. Performance could be slightly lower compared to arrays, but easier to use. |
| Dictionary<TKey, TValue> TKey represents the key, and TValue represents the value | Hashtable | Implemented as a hash table. Values accessed by key. |
| SortedList<TKey, TValue> | SortedList | Implemented as two arrays, one for the key and another for values; allows access by index, and by key. |
| SortedDictionary<TKey, TValue> |  | Implemented as a tree. Generally, better than SortedList, when - adding and removing items into large sets - number of items unknown - populating from unsorted data |
| LinkedList<T> |  | A group of nodes, each node consisting of a data item and a link to the next node. Efficient to insert items, but inefficient to search. |
| Queue<T> | Queue | A FIFO (first in, first out) list |
| Stack<T> | Stack | A LIFO (last in, first out) list |

我们将查看两种性能总体良好的无序泛型集合：

+   1. List<T>，它不需要唯一的键，以及
+   2. Dictionary<TKey, TValue>，它需要唯一的键。

## 复习问题

9.1 列出两个区分 C# 集合与数组的特性。

9.2 什么是泛型集合？

## 9.2 List<T> 集合

## 示例

```
List<int> unitsSold = new List<int>();        // Creates a List of int type named unitsSold
List<string> movies = new List<string>();      // Creates a List of string type named movies
List<int[]> classGrades = new List<int[]>();   // Creates a List of int arrays named classGrades
List<Array> examScores = new List<Array>();    // Creates a List of arrays named examScores
List<Customer> customers = new List<Customer>(); // Creates a List of Customer type
```

请注意，上述示例中的名称如 unitsSold 和 movies 是引用 List 的变量的名称，虽然为了简洁，我们将它们描述为 List 的名称。

通常，术语“List”用于代替“引用 List 对象的变量”。

## 向 List 添加项目

Add() 方法将指定的项目添加到 List 的末尾。当 List 中的项目数超过其初始容量时，容量会自动加倍。

## 使用上面创建的 Lists 的示例

```
unitsSold.Add(205);        // adds 205 to the end of the unitsSold List
movies.Add("Pocahontas");
int[] studentGrades = {85,91,80};        // creates the array to be inserted into a List
classGrades.Add(studentGrades);          // Adds the array studentGrades to the List, classGrades
```

## 访问项目

一种访问每个元素的方法是指定元素的索引。

## 示例

```
unitsSold[0] returns the int type number stored in the first element of unitsSold
classGrades[0] returns the array stored in the first element of classGrades
```

你也可以使用 foreach 循环来访问 List 的每个元素。

## 教程 1：使用 List 查找销售数据

让我们看一个示例，类似于第 8 章中讨论的示例，用于查找指定产品号的销售数据。产品号和第 1-4 季度销售数据从文本文件 Sales.txt 中读取，如图 9-1 所示。每行中的第一个数据项是产品号，其后是第 1-4 季度的销售数据。

图 9-1：Sales.txt 文件

```
1033, 16, 32, 23, 40
1009, 144, 182, 169, 205
1014, 54, 49, 72, 63
1005, 38, 62, 55, 77
1001, 7, 9, 8, 15
1025, 98, 110, 105, 130
```

在第 8 章中，我们使用 2-D 数组来存储数据。在此应用程序中，你将使用泛型 List 来存储数据并帮助查找指定产品的全年总销售额。产品号从 ComboBox 中选择，总销售额显示在 ListBox 中，如图 9-2 所示。

图 9-2：GenericList 表单

![](img/143bad48262566137acc9c41f668a88f_298_0.png)

此表单的编码由三部分组成：

+   1. 创建一个名为 sales 的 List。
+   2. 从 Sales.txt 读取每一行，将其拆分并存储在临时数组中，然后将数组添加到 List。将产品号添加到 ComboBox。两个任务都在表单的 Load 事件处理程序中完成。
+   3. 当用户从 ComboBox 中选择产品号时，从 List 中查找对应的项目。这是在 ComboBox 的 SelectedIndexChanged 事件中完成的。

## 创建 List

步骤 1-1：打开 Tutorial_Starts 文件夹中的项目 Ch9_Collections。打开如图 9-2 所示的表单 GenericList。

步骤 1-2：创建由变量 sales 引用的字符串数组的 List，如图 9-3 第 21 行所示。这是在类级别声明的，以便 List 可以在 Load 事件和 SelectedIndexChanged 事件中使用。List 的类型为 string[]，尽管产品号和售出单位是整数，因为从文本文件读取的数据是字符串类型。

## 图 9-3：创建由变量 sales 引用的 List 的代码

```
17    public GenericList()
18    {
19        InitializeComponent();
20    }
21    private List<string[]> sales = new List<string[]>();
```

图 9-4 显示了读取 Sales.txt 中的每一行、将其拆分并存储在临时数组中，然后将数组添加到 List 的代码的第 2 部分。除了第 36 行外，代码与你之前用于从文本文件读取每一行并存储在名为 fields 的数组中的示例代码相同。代码还将产品号添加到 ComboBox。

## 图 9-4：向 List 和 ComboBox 添加项目的代码

```
22
23    private void GenericList_Load(object sender, EventArgs e)
24    {
25        string currentLine;
26        string[] fields = new string[2];
27        //Create StreamReader
28        StreamReader SalesReader = new StreamReader("Sales.txt");
29
30        //Read each line from the file, split and store in an array
31        while (SalesReader.EndOfStream == false)
32        {
33            currentLine = SalesReader.ReadLine(); // Read a product# and four sales data
34            fields = currentLine.Split(','); // Store Product# and Sales in a temp array
35
36            sales.Add(fields);                // Add the entire array to the List, sales.
37            cboProdNumber.Items.Add(fields[0]); // Add product# to the ComboBox
38        }
39        SalesReader.Close();
40    }
```

第 36 行将数组 fields 添加到 List。数组由产品号和第 1-4 季度的销售数据组成。图 9-5 显示了将文件第一行添加到 List 后的 List。

## 图 9-5：sales List 在添加第一个项目后

| Index |  |  |  |  |  |
|---|---|---|---|---|---|
| 0 | 1033 | 16 | 32 | 23 | 40 |
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |

## 使用索引在 List 中查找项目

当 ComboBox 和 List 都未排序时，或当两者都已排序时，两者都以相同的顺序存储产品号，因为它们是从 Sales.txt 文件中以相同的顺序添加的。这意味着 ComboBox 中所选产品的索引与 List 中对应项目的索引相同。因此，ComboBox 的 SelectedIndex 可用作 List 的索引来查找项目。

例如，如果你从 ComboBox 中选择产品号 1014，SelectedIndex 将为 2，并且 sales[2] 将为你提供四个季度销售的对应数组。

图 9-8 显示了使用 ComboBox 的 SelectedIndex 查找季度销售并求出四个季度销售总和的代码。

## 图 9-8：使用所选项目的索引查找项目的代码

```
private void cboProdNumber_SelectedIndexChanged(object sender, EventArgs e)
{
    string fmtStr = "{0,-20}{1,8}";
    lstDisplay.Items.Clear();
    lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Total Sales"));

    // If both the List and ComboBox are not sorted, or if both are sorted, then
    // you can use the SelectedIndex from the ComboBox to find the item from the List:
    int selectedIndex = cboProdNumber.SelectedIndex;
    string[] productSale = sales[selectedIndex];

    // compute total sales for quarters 1 - 4
    int annualSales = 0;
    for (int quarter = 1; quarter <= 4; quarter++)
        annualSales = annualSales + int.Parse(productSale[quarter]);

    lstDisplay.Items.Add(string.Format(fmtStr, cboProdNumber.SelectedItem, annualSales));
```

第 50 行：int selectedIndex = cboProdNumber.SelectedIndex;

上述语句获取 ComboBox 中所选产品的索引并将其存储在 selectedIndex 中。

第 51 行：string[] productSale = sales[selectedIndex];

sales[selectedIndex] 从 selectedIndex 指定的位置获取项目（数组）。此字符串数组存储在 string 数组类型的引用变量 productSale 中。字符串数组 productSales 将有五个元素，索引为 0 - 4，表示产品号和第 1 至第 4 季度的销售数据。

第 55-56 行使用循环将四个季度的销售数据相加以获得全年的总销售额。

步骤 1-5：在 SelectedIndexChaned 事件中添加图 9-8 中的第 50 行和第 51 行的代码。
添加 SelectedIndexChanged 事件中第 55 行和第 56 行的代码以计算年度销售额。

