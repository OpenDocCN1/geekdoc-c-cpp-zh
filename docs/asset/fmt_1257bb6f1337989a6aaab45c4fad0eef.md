
（注：此处原文包含大量重复和损坏的 OCR 内容，已根据可见片段和标准 LINQ 文档重构了逻辑。）

```csharp
new Customer() { FirstName="Bob", LastName="Boggart",
Balance = 150, DueDate = new DateTime(2020, 2, 5),
// Other Customers omitted ...
}
```

```csharp
// 显示所有客户。
allListBox.DataSource = customers;
```

```csharp
// 显示余额为负的客户
var negativeQuery =
from Customer cust in customers
where cust.Balance < 0
select cust;
negativeListBox.DataSource = negativeQuery.ToArray();
```

```csharp
// 显示欠款至少 50 的客户。
var owes50Query =
from Customer cust in customers
where cust.Balance <= -50
select cust;
owes50ListBox.DataSource = owes50Query.ToArray();
```

```csharp
// 显示欠款至少 50
// 且逾期至少 30 天的客户。
var overdueQuery =
from Customer cust in customers
where (cust.Balance <= -50) &&
(DateTime.Now.Sub(cust.DueDate).TotalDays > 30)
select cust;
overdueListBox.DataSource = overdueQuery.ToArray();
```

程序开始时创建一个 `DateTime` `today` 并将其设置为 2020 年 4 月 1 日。在实际应用程序中，你可能会使用当前日期（已注释掉），但这里使用了特定日期，以便与示例数据匹配。程序在标题栏中显示日期（以便你可以与客户的截止日期进行比较），并创建一个 `Customer` 对象的数组。

接下来的代码将 `listBox` 控件的 `DataSource` 属性设置为该数组，以便 `ListBox` 显示所有的 `Customer` 对象。`Customer` 类重写的 `ToString` 方法会显示每个客户的名称、余额和截止日期。

程序执行了以下 LINQ 查询：

```csharp
// 显示余额为负的客户
var negativeQuery =
from Customer cust in customers
where cust.Balance < 0
select cust;
negativeListBox.DataSource = negativeQuery.ToArray();
```

该查询使用了 `where` 子句筛选 `Balance` 属性小于 0 的客户。查询返回一个 `IEnumerable`，但 `ListBox` 的 `DataSource` 需要 `IList` 或 `IListSource`，而 `IEnumerable` 并不满足这两个接口中的任何一个。为了解决这个问题，程序调用了结果的 `ToArray` 方法将其转换为 `DataSource` 属性可以处理的数组。

在显示此结果后，程序执行了两个 LINQ 查询并以的方式的方式了它们的结果。第一个查询选择了欠款至少 50 的客户。最后一个查询选择了欠款至少 50 且 `DueDate` 超过过去 30 天的客户。

# 排序子句

通常情况下，如果对选定的值进行排序，查询结果将更容易阅读。你可以通过在 `where` 子句和 `select` 子句之间插入排序子句来实现。

排序子句以关键字 `orderby` 开头，后面跟着一个或多个用逗号分隔的值，这决定了结果的排序方式。

可选地，可以在值后面跟随 `ascending`（升序）或 `descending`（降序），以决定结果按升序（1-2-3 或 A-B-C）还是降序（3-2-1 或 C-B-A）排列。

例如，以下查询选择了余额为负的客户，并对其进行排序，使数值最小（负值最大）的客户在前面：

```csharp
var negativeQuery =
from Customer cust in customers
where cust.Balance < 0
orderby cust.Balance ascending
select cust;
```

以下版本按余额对结果排序，如果两个客户的余额相同，则按姓排序：

```csharp
var negativeQuery =
from Customer cust in customers
where cust.Balance < 0
orderby cust.Balance, cust.LastName
select cust;
```

# 选择子句

`select` 子句决定了从数据源中提取并存储在结果中的哪些数据。之前所有的示例都选择了它们所范围范围的数据。例如，“查找客户”示例程序在 `Customer` 对象的数组上进行范围，并选择了特定的 `Customer` 对象。

程序不仅可以选择查询范围内的对象，还可以选择这些对象的某些属性、从这些属性计算出的结果，甚至是全新的对象。从现有数据中选择新类型的数据被称为数据的转换或投影。

图 36-2 所示的“查找学生”示例程序（可在本课程网站的代码加载中找到）使用了以下 `student` 类：

```csharp
class Student {
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public List<int> TestScores { get; set; }
}
```

程序使用以下查询按姓名选择所有学生的姓名和测试平均分：

```csharp
// 按姓名排序选择所有学生及其测试平均分。
var allStudents =
    from student in students
    order by student.LastName, student.FirstName
    select student.Format("{0} {1}|{2:0.00}", student.FirstName, student.LastName, student.TestScores.Average());
ListBox.DataSource = allStudents.ToArray();
```

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_544_0.png)

图 36-2

该查询的 `select` 子句没有选择范围变量 `student`。相反，它选择了一个包含学生姓名和测试得分平均分的字符串。（注意代码是如何调用 `TestScore` 的 `Average` 方法来获取测试分数的平均值的。）查询的结果是一个 `List-string` 而不是 `List`。

在此“尝试一下”（Try It）中，你将修改该程序以使用 LINQ 执行相同的搜索。你无需编写代码来遍历 `GetFiles` 返回的文件并检查每个文件，而是让 LINQ 为你检查这些文件。

## 课程要求

在本节中，

- 复制你为第 29 节“尝试一下”构建的程序（或从书籍网站下载第 29 节的版本），并修改代码使用 LINQ 搜索文件。

> 注意：你可以从网站 `www.wrox.com/csharp24hourtrainer2` 下载本节的代码和资源。

## 提示

- 在查询的 `from` 子句中使用 `DirectoryInfo` 对象的 `GetFiles` 方法。
- 在查询的 `where` 子句中，使用 `File` 类的 `ReadAllText` 方法获取文件内容。将其转换为小写，并使用 `Contains` 检查文件是否包含目标字符串。

## 步骤说明

- 复制你为第 29 节“尝试一下”构建的程序（或从书籍网站下载第 29 节的版本），并修改代码使用 LINQ 搜索文件。

1. 复制程序的操作相当直接。

2. 要使用 LINQ 搜索文件，修改搜索按钮的 `Click` 事件处理程序，使其如下所示。**粗体行**显示了修改后的代码：

```csharp
// 搜索匹配模式
// 并包含目标字符串的文件。
private void searchButton_Click(object sender, EventArgs e)
{
    // 获取模式和目标字符串。
    string pattern = patternTextBox.Text;
    string target = targetTextBox.Text.ToLower();

    // 搜索文件。
    DirectoryInfo dirinfo =
        new DirectoryInfo(directoryTextBox.Text);
    var query =
        from FileInfo fileinfo
        in dirinfo.GetFiles(pattern, SearchOption.AllDirectories)
        where File.ReadAllText(fileinfo.FullName).ToLower().Contains(target)
        select fileinfo.FullName;

// 显示结果。
    fileListBox.DataSource = query.ToArray();
}
```

如果你将此代码与第 29 节“尝试一下”使用的版本进行比较，你会发现这个版本要短得多。

## 练习题

1. 构建一个程序，列出目录中文件的名称及其大小，并按从大到小的顺序排序。
2. 复制你为练习 1 构建的程序并修改它，使其从指定的目录开始在目录层次结构中搜索文件。
3. 编写一个程序列出 0 到 999 之间的完全平方数。（提示：使用 `Enumerable` 类的 `Range` 方法初始化源数据。）

对于练习 4 到 8，请下载客户订单（Customer Orders）程序。该程序定义了以下类：

```csharp
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

程序的 `Form_Load` 事件处理程序创建了一个 `Order` 对象的数组。如图 36-3 所示的程序按钮允许用户以各种方式显示数据，而其中不包含任何代码。在练习 4 到 8 中，你将添加代码以为程序提供功能。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_548_0.png)

图 36-3

> 注意：请在 `www.wrox.com/go/csharp24hourtrainer2` 查看第 36 节的在线视频。

# LINQ to SQL

第 36 节介绍了 LINQ to Objects。本节将简要介绍 LINQ 家族的另一种技术：LINQ to SQL。

LINQ to SQL 允许你使用类似于 LINQ to Objects 提供的查询来操作 SQL Server 数据库。它使用一组类来表示数据库对象（如表和记录）。这些类提供了添加、修改和其他操作记录的直观方法。

在本节中，你将学习 LINQ to SQL 的基础。你学习了如何创建表示 SQL Server 数据库的 LINQ 对象以及向数据库添加记录。你还学习了如何执行类似于第 36 节描述的查询，以过滤和排序从数据库中提取的数据。

注意，本节描述的程序和技术仅演示了 LINQ to SQL 的简单用法。如需更多信息，请访问 `microsoftdn.com/library/bb36976.aspx` 的“LINQ to SQL”页面，这是学习 LINQ to SQL 的起点。

## 连接数据库

创建 LINQ to SQL 程序的第一步是连接数据库。照常创建一个 Windows Forms 应用程序。然后打开图 37-1 所示的服务器资源管理器（Server Explorer）（如果找不到，可以使用“视图”菜单中的服务器资源管理器命令）。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_551_0.png)

图 37-1

> 注意：本节描述的大部分程序，需要在计算机上安装 SQL Server。Visual Studio 软件自带 SQL Server（你看到的版本），也可以从 `www.microsoft.com/express` 下载免费的 SQL Server 版本。该页面非常繁忙，下载链接可能很难找到。

> 注意：遗憾的是书中没有足够的空间介绍关于 SQL Server 以及如何使用它。你将依靠网络或购买关于 SQL Server 的书籍来对其进行操作。为了让本节描述的示例更容易，本节下载包含了一个名为 `Build Database` 的程序。该程序连接到你的 SQL Server 实例，如果 `CustomerDatabase` 存在则删除它，并创建一个包含本节示例记录的 `CustomerDatabase`。如果你已经有了 `CustomerDatabase` 的数据库，显然不要运行此程序，因为数据库会被破坏！

点击“连接数据库”按钮（图 37-1 顶部左侧第三个），显示图 37-2 所示的连接对话框。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_552_0.png)

图 37-2

最初，连接对话框选择了 SQL Server 以外的数据库类型。图 37-2 所示的对话框准备连接 Access 数据库。切换到 SQL Server，点击“更改”按钮显示图 37-3 所示的对话框。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_552_1.png)

图 37-3

选择 Microsoft SQL 条目并点击确定。当你返回连接对话框时，它看起来应该像图 37-4。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_553_0.png)

图 37-4

在指定的文本框中输入你的服务器名称。如果你运行的是 Express 版本，请在服务器名称后加上 `\SQLEXPRESS`，例如，我的计算机名为 Quark，我运行的是 Server 版本，因此我在图 37-4 中输入了 `QUARK\SQLEXPRESS`。

输入服务器上的数据库名称（我在图 37-4 中输入了 `CustomerDatabase`）并点击确定。

> 注意：在图 37-4 所示的对话框中，如果你输入的数据库名称在服务器上不存在，Visual Studio 会告诉你数据库不存在并询问你是否想要创建它。如果你点击“是”，可以使用服务器资源管理器生成数据库。服务器资源管理器提供的功能没有 SQL Server Management Studio 这样的数据库管理工具那么丰富，但如果你无法方便访问那些工具，它就很有用。

如果你回到图 37-1，你可以看到展开了 `quark\sqxpress` 服务器的服务器资源管理器，显示了它的单表 Customers 及其列。

> 注意：你可以使用类似的步骤连接其他类型的数据库，如 Oracle、MySQL 或 Microsoft Access 数据库。只是连接对话框所需的细节不同。例如，图 37-2 显示了 Microsoft Access 数据库所需的细节，而图 37-4 显示了 SQL Server 数据库所需的细节。

注意，LINQ to SQL 旨在与 SQL Server 工作，使其在其他类型数据库上运行需要一些额外工作。本节后面的“在 Access 中使用 LINQ to SQL”部分解释了如何对 Access 数据库使用 LINQ to SQL 类，但不能保证相同的技术适用于每种数据库，也无法保证技术在 Visual Studio 的后续版本中将继续有效。

## 创建 LINQ to SQL 类

在建立数据库连接后，你就可以准备构建用于操作数据库的 LINQ to SQL 类。

打开“项目”菜单并选择“添加新项”。选择 LINQ to SQL 类模板。如果你很难找到它，可以通过查看左侧的“数据”模板来导航搜索。为新文件输入一个描述性名称 `CustomerClasses` 并点击添加。

此时，Visual Studio 创建了一个 `.dbml` 文件来管理新的 LINQ to SQL 类。它会在图 37-5 所示的对象关系设计器中打开，尽管设计器是空的。

在服务器资源管理器中，展开你的数据库直到找到表，并将你想管理的表拖入到设计器表面。在图 37-5 中，我将 Customers 表拖入到表面，因此设计器创建了一个表示该表的类。该类的每个实例将代表表中的行。

设计器将表的字段表示为属性。仔细观察图 37-5，你可以看到表的主键字段 FirstName 和 LastName 左侧有小符号。

如果你点击设计器中的字段，属性窗口将显示该字段的属性。图 37-6 显示了表 FirstName 字段的属性。

# 516 | 第 37 节 LINQ TO SQL

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_555_0.png)

图 37-5
