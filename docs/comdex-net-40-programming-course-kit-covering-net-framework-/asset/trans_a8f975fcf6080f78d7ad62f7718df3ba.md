
```vb
Public Name As String
End Class
Public Class Order
    Public Key As Integer
    Public Order As String
End Class
```

清单 7.16 中突出显示的代码片段展示了 **Customer** 和 **Order** 类的定义。**Customer** 类有两个变量 **Key** 和 **Name**，它们使用 **Public** 访问修饰符声明。类成员的访问修饰符指示可访问该成员的范围。你可以在 *VB 2010* 部分的第 2 章 *面向对象编程* 中进一步了解访问修饰符。**Order** 类也有两个变量 **Key** 和 **Order**，它们使用 **Public** 访问修饰符声明。

- 11. *双击*窗体，为其 *Load* 事件创建事件处理程序，并将清单 7.17 中突出显示的代码片段添加到代码编辑器。

**清单 7.17：处理窗体的 Load 事件**

```vb
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    Dim customers = New List(Of Customer)(New Customer() {New Customer With {.Key = _
        1, .Name = "John"}, New Customer With {.Key = 2, .Name = "Peter"}, _
        New Customer With {.Key = 3, .Name = "David"}, New Customer With {.Key = 4, _
        .Name = "Mark"}, New Customer With {.Key = 5, .Name = "Steve"}})
    Dim orders = New List(Of Order)(New Order() {New Order With {.Key = _
        1, .Order = "Order 1"}, New Order With {.Key = 2, .Order = _
        "Order 2"}, New Order With {.Key = 3, .Order = "Order 3"}, _
        New Order With {.Key = 4, .Order = "Order 4"}, New Order With {.Key = 5, _
        .Order = "Order 5"}})
    Dim query = From c In customers Join o In orders On c.Key Equals o.Key _
        Select New With {c.Name, o.Order}
    For Each q In query
        ListBox1.Items.Add(q.Order.ToString() & " --> " & q.Name)
    Next q
End Sub
```

清单 7.17 展示了 Form1 的 Load 事件的事件处理程序代码。在突出显示的代码片段中，我们首先创建一个 **Customer** 对象列表，然后创建另一个 **Order** 对象列表。之后，我们在 LINQ 查询中使用 **Join** 子句，根据两类对象的 **Key** 字段中的值，将 **Customer** 对象与 **Order** 对象联接起来。最后，我们将订单及其各自的客户添加到 **ListBox1** 控件的 **Items** 集合中。

- 12. *按* **F5** 键运行应用程序。应用程序的输出如图 VB-7.26 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_260_0.png)

图 VB-7.26

这是 **Join** 运算符的一个示例；在该示例中，你使用 **Join** 子句联接来自两个不同数据源的数据。

## 量词运算符

量词运算符根据序列中的元素是否满足给定条件返回布尔值（True 或 False）。表 7.9 列出了 LINQ 中的所有量词运算符：

**表 7.9：LINQ 中的量词运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| All | 检查集合中的所有元素是否都满足某个条件 | Aggregate ... In ... Into All(...) |
| Any | 检查集合中是否有任何元素满足某个条件 | Aggregate ... In ... Into Any() |
| Contains | 确定集合是否包含指定元素 | 不可用 |

## 生成运算符

生成运算符有助于创建新的值序列。这意味着已经有一个按特定顺序排列的值集合；不过，你也可以从该集合中选择一个值范围或重复值，并将它们放入另一个序列中。

表 7.10 列出了 LINQ 中的所有生成运算符：

**表 7.10：LINQ 中的生成运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| DefaultIfEmpty | 检索指定集合的元素；如果指定集合为空，则检索默认值 | 不可用 |
| Empty | 返回空集合 | 不可用 |
| Range | 借助给定的值范围创建新集合 | 不可用 |
| Repeat | 通过将单个值重复指定次数来创建新集合 | 不可用 |

## 元素运算符

元素运算符是仅从序列中返回一个元素的运算符。这意味着，当你只想从特定序列中检索一个值时，可以使用元素运算符。

表 7.11 列出了 LINQ 中的所有元素运算符：

**表 7.11：LINQ 中的元素运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| ElementAt | 检索集合中指定索引处的元素。 | 不可用 |
| ElementAtOrDefault | 检索集合中指定索引处的元素；如果指定索引超出范围或不可用，则检索默认值。 | 不可用 |
| First | 检索集合中的第一个元素；或检索集合中满足给定条件的第一个元素。 | 不可用 |
| FirstOrDefault | 检索集合的第一个元素或满足给定条件的第一个元素。如果不存在此类元素，则返回默认值。 | 不可用 |
| Last | 检索集合中的最后一个元素；或检索集合中满足给定条件的最后一个元素。 | 不可用 |
| LastOrDefault | 检索集合中的最后一个元素；或检索集合中满足给定条件的最后一个元素；如果集合中没有元素满足给定条件，则返回默认值。 | 不可用 |
| Single | 从仅包含一个元素的集合中检索该元素；或从集合中检索满足给定条件的元素。 | 不可用 |
| SingleOrDefault | 检索集合中的唯一元素；或检索满足给定条件的唯一元素；如果集合中没有元素满足给定条件，则返回默认值。 | 不可用 |

## 转换运算符

转换运算符用于执行数据类型转换。它们用于将对象从一种类型转换为另一种类型。表 7.12 列出了 LINQ 中的所有转换运算符：

**表 7.12：LINQ 中的转换运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| AsEnumerable | 将集合的数据类型更改为 IEnumerable(Of T) | 不可用 |
| AsQueryable | 将 IEnumerable 或 IEnumerable(Of T) 集合转换为 IQueryable 或 IQueryable(Of T) 集合 | 不可用 |
| Cast | 将集合的数据类型更改为新的数据类型 | From ... As ... |
| OfType | 从一组值中仅选择可转换为指定类型的那些值 | 不可用 |
| ToArray | 将集合转换为数组 | 不可用 |
| ToDictionary | 基于键选择器函数，将 IEnumerable(Of T) 集合转换为 Dictionary(Of T) 集合 | 不可用 |
| ToList | 将集合的数据类型更改为 List(Of T) | 不可用 |
| ToLookup | 基于键选择器函数，从 IEnumerable(Of T) 集合创建 Lookup(Of T Key, TElement) 数据结构 | 不可用 |

## 聚合运算符

聚合运算符用于从集合中计算单个值。聚合的一个示例是计算集合中值的总和。

表 7.13 列出了 LINQ 中的所有聚合运算符：

**表 7.13：LINQ 中的聚合运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| Aggregate | 对一组值执行自定义聚合操作 | 不可用 |
| Average | 计算一组值的平均值 | Aggregate ... In ... Into Average() |
| Count | 统计集合中元素的总数，或集合中满足指定条件的元素数 | Aggregate ... In ... Into Count() |
| LongCount | 统计大型集合中元素的总数，或集合中满足指定条件的元素数 | Aggregate ... In ... Into LongCount() |
| Max | 从一组值中查找最大值 | Aggregate ... In ... Into Max() |
| Min | 从一组值中查找最小值 | Aggregate ... In ... Into Min() |
| Sum | 计算集合中值的总和 | Aggregate ... In ... Into Sum() |

## 相等运算符

相等运算符检查两个序列是否相等，并且两个序列具有相同数量的元素。表 7.14 列出了 LINQ 中的相等运算符：
