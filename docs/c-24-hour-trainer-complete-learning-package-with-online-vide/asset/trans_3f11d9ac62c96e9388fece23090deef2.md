
```
    // Display the result.
    fileListBox.DataSource = fileQuery.ToArray();
    }
```

如果你将这段代码与第 29 课 Try It 中使用的版本进行比较，就会发现这个版本短得多。

### 练习

- 1. 编写一个程序，列出目录中文件的名称及其大小，按文件从大到小排序。
- 2. 复制你在练习 1 中编写的程序并修改它，使其从指定的目录开始在目录层次结构中搜索文件。
- 3. 编写一个程序，列出 0 到 999 之间的完全平方数。 （提示：使用 Enumerable 类的 Range 方法初始化源数据。）

对于练习 4 到 8，下载 Customer Orders 程序。该程序定义了以下类：

```
    class Person
    {
        public string Name { get; set; }
    }

    class OrderItem
    {
        public string Description { get; set; }
        public int Quantity { get; set; }
        public decimal UnitPrice { get; set; }
    }

    class Order
    {
        public int OrderId { get; set; }
        public Person Customer { get; set; }
        public List<OrderItem> OrderItems { get; set; }
    }
```

程序的 Form_Load 事件处理程序创建一个 Order 对象数组。程序的按钮如图 36-3 所示，可让用户以各种方式显示数据，尽管最初它们不包含任何代码。在练习 4 到 8 中，你添加该代码以赋予程序其功能。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_548_0.png)

图 36-3

- 4. Customer Orders 程序创建了多个 Order 对象，但它没有填充这些对象的 TotalCost 属性。使用 LINQ 来完成此操作。 （提示：使用 foreach 循环遍历对象。对于每个对象，使用 LINQ 查询遍历订单的 OrderItems 列表并选择每个 OrderItem 的 UnitPrice 乘以其 Quantity。定义查询后，调用其 Sum 函数以获取订单的总成本。）
- 5. 复制你在练习 4 中编写的程序并在 All Orders 按钮后面添加代码。该代码应使用 LINQ 查询选择订单的 ID、客户姓名和总成本。通过将该控件的 DataSource 属性设置为查询，在 resultListBox 中显示结果。
- 6. 复制你在练习 5 中编写的程序并在 Order By Cost 按钮后面添加代码。该代码应使用与练习 5 中使用的类似查询，但应按成本对结果进行排序，以便成本最大的订单排在最前面。
- 7. 复制你在练习 6 中编写的程序并在 Customer 按钮后面添加代码。该代码应使用 LINQ 查询列出在 ComboBox 中选择的客户下的订单。 （如果未选择名称，则不执行任何操作。）
- 8. 复制你在练习 7 中编写的程序并在 Greater Than 按钮后面添加代码。该代码应使用 LINQ 查询列出总成本大于在 TextBox 中输入的值的订单。

**注意** 请在 www.wrox.com/go/csharp24hourtrainer2evideos 在线选择第 36 课的视频。

## 37 LINQ to SQL

第 36 课提供了 LINQ to Objects 的介绍。本课简要介绍了 LINQ 系列技术中的另一种技术：LINQ to SQL。

LINQ to SQL 让你可以使用与 LINQ to Objects 提供的类似查询来操作 SQL Server 数据库。它使用一组类来表示数据库对象，例如表和记录。这些类提供了直观的方法来添加、修改、删除以及以其他方式操作记录。

在本课中你将学习 LINQ to SQL 的基础知识。你将学习如何创建代表 SQL Server 数据库的 LINQ 对象以及如何向数据库添加记录。你还将学习如何执行与第 36 课中描述类似的查询，以过滤和排序从数据库中获取的数据。

请注意，本课中描述的程序和技术仅演示了 LINQ to SQL 的非常简单的用法。如需更多信息，请搜索网络。Microsoft 的“LINQ to SQL”页面 at msdn.microsoft.com/library/bb386976.aspx provides a good starting point for learning more about LINQ to SQL。

### 连接到数据库

创建 LINQ to SQL 程序的第一步是连接到数据库。像往常一样创建一个 Windows Forms 应用程序。然后打开如图 37-1 所示的 Server Explorer。 （如果找不到，请使用 View 菜单的 Server Explorer 命令。）

![](img/d5be6ade75773ca6cec5c78f96a98bb1_551_0.png)

图 37-1

> **注意** 要运行本课中描述的大多数程序，你需要在计算机上安装 SQL Server。Visual Studio 安装软件附带 SQL Server（至少我见过的版本）或你可以从 www.microsoft.com/express/Database 下载免费的 SQL Server Express 版。这是一个相当繁忙的页面，因此下载链接可能很难看到。你可以通过搜索“Express”找到它。

> **注意** 很遗憾，这本书里没有太多篇幅来讲述 SQL Server 以及如何使用它。你必须依赖网络或获取一本关于 SQL Server 的书籍才能做更多事情。
>
> 为了让本课中描述的示例更容易使用，本课的下载包含一个名为 Build Customer Database 的程序。该程序连接到你的 SQL Server 实例，如果存在则删除名为 CustomerDatabase 的数据库，并创建一个新的 CustomerDatabase，其中包含一些记录供本课中描述的示例使用。
>
> 显然，如果你已经有一个名为 CustomerDatabase 且想要保留的数据库，请不要运行此程序，因为该数据库将被销毁！

单击 Connect to Database 按钮（图 37-1 顶部从左数第三个）以显示如图 37-2 所示的 Add Connection 对话框。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_552_0.png)

图 37-2

最初，Add Connection 对话框可能选择了除 SQL Server 之外的某种类型的数据库。图 37-2 所示的对话框已准备好连接到 Microsoft Access 数据库。要切换到 SQL Server，请单击 Change 按钮以显示如图 37-3 所示的对话框。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_552_1.png)

图 37-3

选择 Microsoft SQL Server 条目并单击 OK。返回 Add Connection 对话框时，它应如下图 37-4 所示。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_553_0.png)

图 37-4

在指示的文本框中输入服务器名称。如果你在运行 SQL Server Express Edition，请在服务器名称后加上 \SQLEXPRESS，如图所示。例如，我的计算机名为 QuarkBeast，我运行的是 SQL Server Express Edition，所以我在图 37-4 中输入了 QUARKBEAST\SQLEXPRESS。

输入服务器上的数据库名称（我在图 37-4 中输入了 CustomerDatabase）并单击 OK。

> **注意** 在图 37-4 所示的对话框中，如果你输入服务器上不存在的数据库名称，Visual Studio 会告诉你数据库不存在并询问是否要创建它。如果单击 Yes，你可以使用 Server Explorer 构建数据库。Server Explorer 提供的功能不如 SQL Server Management Studio 等数据库管理工具那么多，但在你无法轻松访问这些工具时非常方便。

如果你返回图 37-1，可以看到 Server Explorer，其中 quarkbeast\sqlexpress 服务器的 CustomerDatabase 已展开，显示其唯一的表 Customers 及其列。

> **注意** 你可以使用类似的步骤连接到其他类型的数据库，例如 Oracle、MySQL 或 Microsoft Access 数据库。唯一不同的是 Add Connection 对话框中连接数据库所需的详细信息。例如，图 37-2 显示了 Microsoft Access 数据库所需的详细信息，而图 37-4 显示了 SQL Server 数据库所需的详细信息。
>
> 请注意，LINQ to SQL 旨在与 SQL Server 配合使用，使其与其它类型的数据库配合使用需要额外的工作。本课后面“使用 LINQ to SQL 与 Access”部分解释了如何使用 LINQ to SQL 类与 Access 数据库一起使用，但不能保证相同的技术适用于每种类型的数据库，也不能保证这些技术在 Visual Studio 的后续版本中仍然有效。

### 创建 LINQ to SQL 类

在建立数据库连接后，你就可以构建可用于操作数据库的 LINQ to SQL 类。

打开 Project 菜单并选择 Add New Item。在 Add New Item 对话框中，选择 LINQ to SQL Classes 模板。如果找不到，可以通过在左侧查看 Data 模板类别来缩小搜索范围。为新文件输入描述性名称，例如 CustomerClasses，然后单击 Add。

此时 Visual Studio 创建一个 .dbml 文件来管理新的 LINQ to SQL 类。它在如图 37-5 所示的 Object Relational Designer 中打开该文件，尽管最初设计器是空白的。

在 Server Explorer 中，展开数据库直到找到其表，然后将要管理的表拖到设计器表面。在图 37-5 中，我将 Customers 表拖到表面上，因此设计器创建了一个代表该表的类。类的每个实例将代表表中的一行。

设计器将表的字段表示为属性。如果仔细查看图 37-5，可以看到表的 primary key 字段 FirstName 和 LastName 在左侧有小钥匙符号。

如果你在设计器中单击一个字段，Properties 窗口将显示该字段的属性。图 37-6 显示了表 FirstName 字段的属性。
