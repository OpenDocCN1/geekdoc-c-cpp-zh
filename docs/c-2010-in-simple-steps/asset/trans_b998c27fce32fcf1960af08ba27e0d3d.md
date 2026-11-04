
在图 C#10.2 中，你可以看到，单击 Click 按钮时，listView1 列表视图会显示能被 2 整除的数字。

现在，我们将在以下各节中讨论 LINQ 中可用的标准查询运算符。

# 探索标准查询运算符

标准查询运算符是用于根据查询和应用程序需求创建并细化数据的子句。标准查询运算符可以视为可用于对任何 .NET 数组或集合执行查询的方法。一些标准查询运算符包括筛选、投影、分区、分组、聚合和排序。LINQ 中的标准查询运算符是一个应用程序编程接口 (API)，可用于查询任何 .NET 数组、集合或数据序列。

LINQ 中可用的各种标准查询运算符在执行查询所需的时间上彼此不同。该时间取决于它们必须返回单个值还是值序列。返回单个值的方法会立即执行，而返回值序列的方法会在返回输出之前重新安排查询的执行。

表 10.1 列出了 LINQ 中使用的标准查询运算符：

表 10.1：LINQ 中的标准查询运算符

| 运算符类型 | 描述 |
|---|---|
| 排序运算符 | 更改查询返回的序列中元素的顺序 |
| 集合运算符 | 以集合形式返回结果集 |
| 筛选运算符 | 限制结果集只包含满足特定条件的元素 |
| 量词运算符 | 返回布尔值，即 True 或 False |
| 投影运算符 | 将对象转换为新对象 |
| 分区运算符 | 将输入序列分成两部分并返回其中一部分 |
| 联接运算符 | 合并集合 |
| 分组运算符 | 将数据排列成组 |
| 生成运算符 | 创建新的值序列 |
| 元素运算符 | 从集合中返回单个特定元素 |
| 转换运算符 | 将集合转换为数组 |
| 聚合运算符 | 从集合计算单个值 |
| 相等运算符 | 检查两个序列是否相等 |
| 串联运算符 | 将一个元素序列追加到另一个序列 |

现在，我们将在以下各节中逐一详细讨论前面的标准查询运算符。

# 排序运算符

LINQ 中的排序运算符根据一个或多个属性对序列中的元素进行排序。你可以根据一个特定属性对序列中的元素排序，并对元素执行主排序。然后，你可以指定第二排序条件，并在主排序组内对元素排序。LINQ 中重要的排序运算符是 orderby 和 orderby descending 子句。

排序功能通过使用 orderby 子句来实现。排序运算符可以按升序或降序对数据排序。orderby 子句的默认行为是按升序对数据排序。如果要按降序对数据排序，需要使用 orderby descending 子句。

现在，让我们创建一个名为 SortingOperator 的 Windows 应用程序，你可以在其中使用 orderby 和 orderby descending 子句对数据排序。为此，请执行以下步骤：

- 1. 重复本章“解释 LINQ 查询及其执行”一节中创建 LINQQuery 应用程序时前面所示的步骤 1 到 3。
- 2. 在 Name 文本框中输入 SortingOperator 以指定应用程序名称，并在 Location 组合框中输入应用程序的适当位置。
- 3. 单击 OK 按钮。SortingOperator 应用程序即创建完成。
- 4. 向 Form1 添加一个 ListView 控件和两个 Button 控件。
- 5. 将 ListView 控件的 Location 和 Size 属性分别更改为 35, 31 和 214, 117。
- 6. 将 button1 和 button2 控件的 Text 属性分别更改为 Ascending 和 Descending。
- 7. 将代码清单 10.2 中给出的代码添加到 button1 控件的 Click 事件中：
- 8. 将代码清单 10.3 中的代码添加到 button2 控件的 Click 事件中：
- 9. 按 F5 键运行应用程序。
- 10. 单击 Ascending 按钮，如图 C#10.3 所示：

### 代码清单 10.2：在 SortingOperator 应用程序中为 button1 控件的 Click 事件添加代码

```csharp
double[] doubles = { 500, 700, 100, 200, 400, 600, 900, 300, 800 };
listView1.Items.Clear();
var sorting = from d in doubles
orderby d
select d;
foreach (var d in sorting)
{
    listView1.Items.Add(d.ToString());
}
```

### 代码清单 10.3：在 SortingOperator 应用程序中为 button2 控件的 Click 事件添加代码

```csharp
double[] doubles = { 500, 700, 100, 200, 400, 600, 900, 300, 800 };
listView1.Items.Clear();
var descendingSorting = from d in doubles
orderby d descending
select d;
foreach (var d in descendingSorting)
{
    listView1.Items.Add(d.ToString());
}
```

代码清单 10.2 中的代码在单击 Ascending 按钮时按升序对数字排序，代码清单 10.3 中的代码在单击 Descending 按钮时按降序对数字排序。

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_310_0.png)

如你在图 C#10.3 中所见，数字按升序排列。

# 集合运算符

LINQ 中的集合运算符用于执行查询操作，这些操作产生的结果集基于同一集合或不同集合中是否存在等效元素。Distinct()、Union()、Intersect() 和 Except() 方法称为 LINQ 中的集合运算符。

Distinct() 方法从一组值中移除重复值。Union() 方法用于返回结果集，该结果集通过合并两个集合中出现的元素而形成。使用 Union() 方法返回的结果集不包含任何重复元素。Intersect() 方法返回两个集合中的公共元素。Except() 方法返回一个集合中未出现在第二个集合中的元素。

# 筛选运算符

筛选，顾名思义，是指对结果集进行筛选，使其仅包含满足指定条件的元素的操作。where 子句在 LINQ 中用作筛选运算符。此子句根据给定条件筛选序列。它用于指定在查询表达式中返回数据源中的哪些元素。

现在，让我们创建一个 Windows 应用程序 FilteringOperator，你可以在其中使用 where 子句。为此，请执行以下步骤：

- 1. 重复本章“解释 LINQ 查询及其执行”一节中创建 LINQQuery 应用程序时前面所示的步骤 1 到 3。
- 2. 在 Name 文本框中输入 FilteringOperator 以指定应用程序名称，并在 Location 组合框中输入应用程序的适当位置。
- 3. 单击 OK 按钮。FilteringOperator 应用程序即创建完成。
- 4. 向 Form1 添加一个 ListView 控件和一个 Button 控件，并将 button1 的 Text 属性更改为 Click。
- 5. 将 ListView 控件的 Location 和 Size 属性分别更改为 12, 12 和 260, 190。
- 6. 将代码清单 10.4 中给出的代码添加到 button1 控件的 Click 事件中：

### 代码清单 10.4：在 FilteringOperator 应用程序中为 button1 控件的 Click 事件添加代码

```csharp
int[] numbers = { 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70,
75, 80, 85, 90, 95 };
var myNums =
from n in numbers
where n > 25
select n;
foreach (var x in myNums)
{
    listView1.Items.Add(x.ToString());
}
```

代码清单 10.4 中的代码生成大于 25 的数字，这是 where 子句中指定的条件。

- 7. 按 F5 键运行应用程序。
- 8. 单击 Click 按钮，如图 C#10.4 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_311_0.png)

图 C#10.4
