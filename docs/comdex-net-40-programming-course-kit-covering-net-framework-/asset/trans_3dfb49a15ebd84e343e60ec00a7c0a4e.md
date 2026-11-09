
**表 7.14：LINQ 中的相等运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| SequenceEqual | 确定两个集合是否相等 | 不可用 |

## 串联运算符

串联运算符允许将两个或多个序列合并为单个序列。表 7.15 列出了 LINQ 中的串联运算符：

**表 7.15：LINQ 中的串联运算符**

| 运算符 | 说明 | 查询表达式语法（Visual Basic） |
|---|---|---|
| Concat | 将一个序列追加到另一个序列，并返回单个序列作为结果 | 不可用 |

## Zip 运算符

Zip 运算符是 ASP.NET 4.0 中 LINQ 引入的新运算符，有助于合并两个集合。该运算符有助于将长度相同的两个序列合并为一个。Zip 运算符使用元素顺序来组合两个给定序列中的元素。这意味着 Zip 运算符从第一个源中取一个元素，并从第二个源中取同一位置的元素，并返回组合类型。

执行以下步骤在 Visual Basic 中实现 Zip 运算符。

- 1. *启动 Visual Studio 2010。*
- 2. *从菜单栏选择* **文件→新建→项目**。**新建项目** *对话框打开。*
- 3. *从“新建项目”对话框左窗格的* **已安装的模板** *部分中选择* **Visual Basic→Windows**。
- 4. *在中间窗格中选择* **Windows 窗体应用程序** *以创建 Windows 窗体应用程序。*
- 5. *在* **Name** 文本框中*输入*应用程序名称 **ZipOperator**（也可在 CD 上找到），并在 **Location** 组合框中输入应用程序的适当位置。
- 6. *单击* **OK** *按钮关闭“新建项目”对话框。* **ZipOperator** *应用程序创建完成。*
- 7. *从工具箱拖放*一个 **ListBox** *和一个* **Button** *控件到窗体上。*
- 8. *将 Button 控件的* **Text** *属性设置为* **Display**。
- 9. *双击* Display 按钮，并*添加*清单 7.18 中所示的以下代码片段到代码编辑器：

**清单 7.18：** 处理 Button1 的 Click 事件

```
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
Handles Button1.Click
    Dim names As String() = New String() {"Ram", "Priya", "Puja", "Rita", "Jhonny", "Steve"}
    Dim position As String() = New String() {"Manager", "Team Leader", "Developer", "Writer", "Director"}
    Dim years As Integer() = New Integer() {1, 2, 4, 8, 9}
    Dim q = names.Zip(position, Function(a, b) a & " is the " & b & " of the company")
    Dim r = q.Zip(years, Function(c, d) c & " with " & d & " years of experience.")
    For Each result In r
        ListBox1.Items.Add(result)
    Next result
End Sub
```

在清单 7.18 中，我们声明了三个数组，其中两个是 **String** 类型，即 **names** 和 **position**，一个是 **Integer** 类型，即 **years**。然后，我们使用 **Zip** 运算符将 **names** 数组值与 **position** 数组组合，并将其赋给 **q**。之后，我们再次使用 **Zip** 运算符组合 **q** 和 **years** 的值。最后，我们使用 **For Each** 循环并将结果添加到 **ListBox1**。

- 10. *按* **F5** 键运行应用程序。
- 11. *单击* **Display** 按钮生成组合输出，如图 VB-7.27 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_265_0.png)

这是 Zip 运算符的一个示例，其中我们可以合并集合并将它们联合显示。

以上就是 LINQ 中使用的标准查询运算符的全部内容。现在让我们了解如何在 ADO.NET 中使用这些运算符。

## 实现 LINQ to ADO.NET

LINQ to ADO.NET 帮助您使用 LINQ 编程模型查询任何 ADO.NET 对象。它由以下三项技术组成：

- **LINQ to DataSet：** 表示对标准 ADO.NET DataSet 编程模型的一组扩展。它允许 **DataSet**、**DataTable** 和 **DataRow** 对象成为 LINQ 查询表达式的自然目标。此外，LINQ to DataSet 提供更丰富且优化的数据集查询。
- **LINQ to SQL：** 允许通过使用实体类移除 ADO.NET 数据类型来与关系数据库交互。这意味着您可以直接与数据库交互，而不是使用 ADO.NET 对象。LINQ to SQL 使您能够直接查询 SQL Server 数据库架构。
- **LINQ to Entities：** 允许为 Entity Framework 概念模型编写查询，使用户能够使用 Visual Studio 2010 和 .NET Framework 4.0 以可视化方式设计模型并映射数据库、表和视图。

现在详细讨论两项重要技术。

### LINQ to DataSet

数据集是数据的内存表示，是各种基于数据的应用程序的核心。将数据加载到数据集后，通常需要对数据执行其他查询。这些附加查询通常通过使用 LINQ to DataSet 技术来执行。

与传统数据查询方法相比，LINQ to DataSet 提供了一种更简单、更快捷的方式来查询缓存在 DataSet 对象中的数据。LINQ to DataSet 通过使您能够用编程语言本身编写查询，简化了查询过程。查询运算符允许您对数据集执行 LINQ 查询。要开始使用 LINQ to DataSet 查询数据集，需要确认数据集是否已填充数据，因为无法从空数据集获得任何输出或结果集。

执行以下步骤在控制台应用程序中实现 LINQ to DataSet：

- 1. *启动* Visual Studio 2010。
- 2. *从菜单栏选择* 文件→新建→项目。**新建项目** 对话框打开。
- 3. *从“新建项目”对话框左窗格的* **已安装的模板** *部分中选择* **Visual Basic→Windows**。
- 4. *在中间窗格中选择* **控制台应用程序** *选项以创建控制台应用程序。*
- 5. *在* **Name** 文本框中*输入*应用程序名称 **LINQToDataSet**（也可在 CD 上找到），并在 **Location** 组合框中输入应用程序的适当位置。
- 6. *单击* **OK** 按钮关闭 **新建项目** 对话框。**LinqToDataSet** 应用程序创建完成。
- 7. *双击* **解决方案资源管理器** 中的 **Module1.vb** 文件，在 **代码编辑器** 中打开该文件，并将清单 7.19 中所示的高亮代码片段添加到 **代码编辑器**。

**清单 7.19：** 向 Module1.vb 文件添加代码

```
Module Module1
    Class Student
        Public Id As Integer
        Public Name As String
    End Class
    Private Function GetDataTable(ByVal students As Student()) As DataTable
        Dim table As DataTable = New DataTable()
        table.Columns.Add("Id", GetType(Integer))
        table.Columns.Add("Name", GetType(String))
        For Each s As Student In students
            table.Rows.Add(s.Id, s.Name)
        Next s
        Return (table)
    End Function
    Sub Main(ByVal args As String())
        Dim students As Student() = {New Student With {.Id = 1, .Name = "A"}, _
            New Student With {.Id = 2, .Name = "B"}, New Student With {.Id = 3, _
            .Name = "C"}, _
            New Student With {.Id = 4, .Name = "D"}, New Student With {.Id = 5, _
            .Name = "E"}, New Student With {.Id = 6, .Name = "F"}}
        Dim dt As DataTable = GetDataTable(students)
        For Each dr As DataRow In dt.Rows
            Console.WriteLine("{0}-{1}-{2}", dr.Field(Of Integer)(0), _
                dr.Field(Of String)(1))
        Next dr
        Console.ReadLine()
    End Sub
End Module
```

清单 7.19 显示了 Module1.vb 文件的代码。在高亮代码片段中，我们首先定义一个类 **Student**，它有两个 **Public** 变量，即 **ID** 和 **Name**。然后，我们定义一个函数 **GetDataTable**，它接受一个 **Student** 对象数组作为参数。之后，我们创建了 **DataTable** 类的一个对象，该对象向数据表添加新行并返回 **DataTable** 类的对象。最后，我们定义 **Sub** 过程 **Main**，它首先创建 **Student** 对象数组，然后通过调用 **GetDataTable** 函数创建 **DataTable** 类的对象，接着在屏幕上显示 **DataTable** 对象的数据。

- 8. *按* **F5** 键运行应用程序。应用程序的输出如图 VB-7.28 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_266_0.png)

图 VB-7.28
