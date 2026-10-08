
在连接到数据源后，不再需要在字符串参数中嵌入 SQL 语句或使用查询生成器存储 `SELECT`、`INSERT`、`DELETE` 或 `UPDATE` SQL 语句，你可以直接在 C# 程序中包含查询表达式。在示例 14-30 中，按照使用数据源配置向导描述的步骤为应用程序附加了数据库。

> 从 `Data` 菜单选项选择了 `Add New Data Source`。使用了 `DataSet` 模型。在提示选择 `Your Database Connection` 时，点击 `New Connection` 按钮允许你选择 `Access` 数据库并浏览其位置。`Access` 数据库被复制到当前项目中。在提示选择 `Database Object` 时，选择了表。然后从 `Data` 菜单选择了 `Show Data Sources` 选项。

![](img/45e6f245af31396d967c3186f196d331_929_0.png)

`Data Sources` 窗口显示了一个 `DataSet` 对象。展开 `Table` 节点显示其数据成员。如果你从 `Data Sources` 窗口拖动表，将自动生成代码。默认情况下，会为 `DataGridView` 对象实例化，并使用表中的每条记录填充 `DataGridView` 对象。对象的

`DataAdapter`、`DataSet`、`TableManager` 和 `TableBindingSource` 也放置在组件箱中，在设计视图中显示在表单下方。当你将表格绘制到表单上时，会自动生成代码将数据加载到 `DataSet` 的表中。该代码位于 `FormLoad()` ) 事件处理程序中。示例 14-30 显示了自动生成的代码。

### 示例 14-30

```
this.memberTableTableAdapter.Fill(this.memberDataSet.MemberTable);
```

与 `DataGridView` 绑定的代码从表中检索所有行。为了演示 LINQ 查询数据库，删除了 `DataGridView` 对象并将 `List` 对象拖动到表单上。查询表达式见示例 14-31。基本上，这里使用了相同的查询表达式。主要的区别在于数据源的标识。

### 示例 14-31

```sharp
private void Form_Load(object sender, EventArgs e)
{
    // TODO: 这行代码将数据加载到
    // 'memberDataSet.MemberTable' 表。
    // 你可以根据需要移动或删除它。
    this.memberTableAdapter.Fill(
        this.memberDataSet.MemberTable);

    var memberResults =
        from member in this.memberDataSet.MemberTable
        where member.LastName.Length > 4
        orderby member.LastName
        select member;

    foreach (var aRecord in memberResults)
        this.lstBxResults.Items.Add(aRecord.FirstName
            + " " + aRecord.LastName);
}
```

示例 14-31 的输出如图 14-38 所示。注意如何使用 `var` 关键字创建 `memberResults` 集合。然后使用 `var` 配合 `foreach` 循环遍历集合并将项添加到列表框。

![](img/45e6f245af31396d967c3186f196d331_931_0.png)

## LINQ to SQL

`LINQ to SQL` 用于查询 SQL 数据库。SQL Server 数据存储在远程服务器上并包含查询引擎。由于 SQL Server 数据库管理系统将数据存储为关系型数据，而 LINQ 与封装在对象中的数据工作，这两种表示必须相互映射。因此，`LINQ to SQL` 定义了一个映射框架。该映射通过定义与数据库表对应的类来完成。指定了 LINQ-to-SQL 定义的属性（如主键）。**`DLinq`**（也称为 `LINQ to SQL`）是专门关注从关系型数据源查询数据的 LINQ 版本。`XLinq` (`LINQ to XML`) 是 LINQ 中倾向于查询 XML 数据的部分。

Visual Studio 包含一个映射设计器，用于创建对象中的数据架构与关系域之间的映射。它可以根据数据库架构自动创建相应的类。

许多书籍都描述了如何使用 C# 和 `.NET Framework` 访问数据库。本章向你介绍了在程序与不同数据源之间建立连接所需的程序语句。它包含了用于从数据库检索和更新数据的程序语句。它还关注了如何使用 IDE 提供的许多视化工具来检索和显示数据。鉴于今天数据驱动应用程序的盛行，强烈鼓励你继续对该主题进行探索。

### 编码规范

- 所有数据库表都应设计为具有主键。你应该在 SQL 查询中作为字段之一检索该键。
- SQL 关键字使用大写字母。
- 在 `UPDATE` 或 `DELETE` 语句的 `WHERE` 条件中使用主键以避免错误。
- 避免在数据库对象的名称中使用空格。

## 资源

你可能感兴趣的额外网站：

- `LINQ to SQL`: 针对关系数据的 .NET 语言集成查询

  http://msdn.microsoft.com/en-us/library/bb425822.aspx

- 101 LINQ 示例

  http://msdn.microsoft.com/en-us/vsharp/aa33746.aspx

- 数据库教程

  http://www.quickkit.com/database/tutorial/

- Access 教程

  http://databases.about.com/od/tutorials/Tutorials.htm

- C# Station ADO.NET 教程

  http://www.csharp-station.com/Tutorials/AdoDotNetLesson01.aspx

2. 以下所有项均为 ADO.NET 数据提供程序的示例，除外：

- a. `OLE DB`
- b. `Oracle`
- c. `ODBC`
- d. `Sql Server`
- e. `Access`

3. 下面哪个用于显示数据库数据的网格结构的类名？

- a. `ComboBox`
- b. `ListBox`
- c. `DataGridView`
- d. `Grid`
- e. `GridData`

4. 数据库将信息存储在记录、字段和以下各项：

- a. 数据提供程序
- b. 网格
- c. 列
- d. 表
- e. 命令

5. 每个数据提供程序提供的核心类包括以下所有，除外：

- a. 连接 (`connection`)
- b. 数据适配器 (`data adapter`)
- c. 命令 (`command`)
- d. 数据集 (`dataset`)
- e. 数据读取 (`data reader`)

6. 每个数据提供程序类通过其进行分组并访问：

- a. 命名空间 (`namespace`)
- b. 数据库 (`database`)
- c. 数据网格 (`datagrid`)
- d. 提供程序 (`provider`)
- e. 系统 (`system`)

# 练习 903

7. 下面哪个是从 `customer` 表检索所有四列的有效 SQL 语句？

- a. `SELECT ALL FROM customer`
- b. `SELECT * FROM customer`
- c. `SELECT customer`
- d. `SELECT ,,, FROM customer`
- e. `SELECT @@ @@ @ FROM customer`

8. SQL Server SQL 语句的参数与为 Access 数据库编写的参数略有不同。在 SQL Server 中，参数使用：

- a. `@` 后跟标识符
- b. 不带标识符的 `@`
- c. `?` 后跟标识符
- d. 不带标识符的 `@`
- e. 一个 `params` 关键字

9. 可以添加到 `SELECT` 语句中以从多个表中检索数据的 SQL 子句是：

- a. `BETWEEN`
- b. `INNER JOIN`
- c. `CROSS JOIN`
- d. `WHERE`
- e. `UPDATE`

10. 以下命名空间（`System.Data.OleDB`, `System.Data.SqlClient`, `System.Data.Odbc`, `System.Data.OracleClient`）包含了用于不同类的：

- a. 数据提供程序
- b. 文件流
- c. `ADO.NET`
- d. 数据库
- e. 数据读取器

11. 对于数据库的只读访问，使用哪种 ADO.NET 类？

- a. `dataset`
- b. `data adapter`
- c. `command builder`
- d. `connection`
- e. `data reader`

12. 为了访问 Access 数据库管理系统，使用哪种数据提供程序？

- a. `System.Data.OleDb`
- b. `System.Data.SqlClient`
- c. `System.Data.Odbc`
- d. `System.Data.OracleClient`
- e. `Microsoft.OLEDB.12.0`

13. 哪个类配合 `dataset` 使用以方便使用离线数据库？

- a. `DataAdapter`
- b. `DataReader`
- c. `Command`
- d. `OleDbConnection`
- e. `Fill`

14. 为了避免编写额外的 SQL 语句来更新实时数据库，你实例化了哪个类的对象？

- a. `DataAdapter`
- b. `DataReader`
- c. `Connection`
- d. `CommandBuilder`
- e. `DataGrid`

15. 为了释放数据库以便其他应用程序可以使用，应该调用哪个方法？

- a. `ReleaseDb()`
- b. `Release()`
- c. `Stop()`
- d. `Close()`
- e. 以上均非

16. 为了从数据库检索特定记录，你可以创建一个新查询并将其存储为哪个类的对象。

- a. `Dataset`
- b. `DataProvider`
- c. `TableAdapter`
- d. `Connection`
- e. `Command`

17. 哪个方法用于最初填充数据绑定的控件？

- a. `Dataset Fill()` 方法
- b. `Dataset Update()` 方法
- c. `TableAdapter Fill()` 方法
- d. `BindingNavigator Save()` 事件
- e. `PageLoad()` 事件

18. 在 Visual Studio 中，允许你连接到数据库并使用 `TableAdapter` 自动填充数据集 对象的向导是：

- a. 数据源配置
- b. 数据源
- c. 查询生成器
- d. `DataSet` 设计器
- e. `TableAdapter` 配置

19. Visual Studio 中使用哪个窗口显示数据集表，以便将其拖放到到表单上？

- a. 服务器资源管理器
- b. 属性
- c. `DataSet` 设计器
- d. 数据源
- e. 解决方案资源管理器

20. 连接字符串包含：

- a. 一个 `using` directive
- b. 数据源名称
- c. 数据库系统的版本号
- d. 数据库中的字段列表
- e. 一个 SQL 语句

21. 解释如何使用数据集、表适配器和数据网格对象来更新数据库。

22. 为以下内容编写 SQL 语句：

- a. 从具有 15 列的 `Parts` 表中检索所有的 `partNumber` 和 `partDescription` 列。
- b. 从表中检索 `partNumbers` 于 1000 到 2000 的记录。仅显示 `partDescription`。
- c. 向 `Customer` 表插入一条新记录。在列中存储以下值：`LName=Osphere`, `FName=Teola`, `CNumber=23456`。列的顺序如下：`CNumber`, `LName`, `FName`。

## 编程练习

23. 当你从 `Data Sources` 窗口将一个数据集表拖到空白表单上时会发生什么？

24. 你如何让控件（默认 `Data Sources` 窗口控件之外）显示数据库表的数据？

25. 表适配器（`table adapter`）与数据适配器（`data adapter`）有何不同？

1. 将数据集表从 `Data Sources` 窗口拖到空白表单上会发生什么？

2. 你如何让控件（默认 `Data Sources` 窗口控件之外）显示数据库表的数据？

3. 表适配器（`table adapter`）与数据适配器（`data adapter`）有何不同？

4. 将数据集表从 `Data Sources` 窗口拖到空白表单上时会发生什么？

5. 你如何让控件（默认 `Data Sources` 窗口控件之外）显示数据库表的数据？

6. 表适配器（`table adapter`）与数据适配器（`data adapter`）有何不同？

# 15

## Web 应用程序

在本章中，你将：

- 发现 Web 应用程序与 Windows 应用程序的不同
- 使用 `ASP.NET` 创建 Web 应用程序
- 开发并配置 Web Forms 页面
- 学习可以添加到 Web 应用程序的不同类型的控件
- 向 Web 应用程序添加 HTML 和 Web Forms 服务器控件
- 添加验证、自定义和复合控件以验证用户输入、显示日历并连接数据库表
- 了解 Web 服务（Web Services）和 Windows 通信框架（WCF) 及其对分布式应用程序的影响
- 学习如何使用 Visual Studio 开发移动应用程序

在之前的章节中，你学习了如何使用 C# 和 Visual Studio 的拖放式构建方法为 Windows 应用程序开发图形用户界面是多么简单。在本章中，你将发现这种方法也可以用于开发 Web 应用程序。你将学习 Web 应用程序的设计与 Windows 应用程序的不同。你将发现 HTML 和 Web 控件之间的差异。你将学习什么是 Web 服务以及如何编写它。本章还介绍了可以在个人数字助手（PDA）等小型个人设备上查看的移动应用程序。

Web 应用程序通常是数据驱动的。在第 14 章中，你学习了用于访问和更新存储在数据库表中的数据的丰富类。你学习了每个数据提供程序中的连接（`connection`）、命令（`command`）、数据读取器（`data reader`）和数据适配器核心。你将在开发的 Web 应用程序中使用这些 ADO.NET 类。你将学习如何使用验证控件来检查用户的输入值。你将学习如何向 Web 页面添加日历控件。当你完成本章时，你将能够创建非常复杂、高度交互且数据驱动的应用程序。

### Web 应用程序

Web 应用程序在浏览器浏览器中运行——这意味着它设计用于多个用户访问，可以在不同平台上运行，并向每个用户交付相同的内容。Web 应用程序简单来说存储在 Web 服务器上的一个或多个相关文件或组件的集合。Web 应用程序也称为网站。Web 服务器是托管或交付 Web 应用程序的软件。加载 Web 服务器软件的硬件通常被称为 Web 服务器，但让设备变得特殊并使计算机能够被称为服务器的是该软件。

## Web 编程模型

Web 页面的编程模型与 Windows 应用程序有些不同，特别是在与用户的交互方面。例如，Windows 应用程序常用的 `MessageBox` 对话框在 Web 应用程序中并不使用。它们的输出显示在服务器计算机上，而不是请求页面的客户端计算机上。访问 Web 页面的用户消息通常通过 `Label` 对象或页面上的其他对象显示。

对 Web 页面的每次请求都需要到存储页面的服务器进行一次往返（round-trip）。这意味着用户通过在 Web 浏览器中输入 Web 地址（即统一资源定位符 `URL`）通过超文本传输协议（`HTTP`）请求页面。该请求被转发到存储该页面的 Web 服务器。页面以超文本标记语言（`HTML`）文档的形式返回，并在请求页面的客户端计算机上被渲染（从 HTML 转换）为格式化页面。

对该页面的第二次及后续请求需要向服务器进行一次回传（postback）。但并不是所有事件在触发时都会自动回传到服务器。某些事件（例如 `ListBox` 和 `RadioButton` 对象的 `SelectedSelectedIndex` 或 `CheckedEvents`）会被排队队列，除非触发了会导致向服务器回传的事件，否则它们的事件处理方法不会执行。`ButtonClick` 是少数引起自动回传的事件之一。

每次向服务器回传都会创建一个新对象。这导致 Web 页面是无状态的——意味着它们不会保留从一次访问 Web 服务器到下一次访问的值。例如，你输入到 `TextBox` 对象中的值在页面发送回客户端计算机时不会被自动保存和重新发现。对该页面的第二次及后续请求可能需要通过程序化方式检索并存储输入的值，然后在页面发送回客户端计算机重新显示时将这些值发送回控件。该编程模型需要一些重要的额外考量。在接下来的章节中，你将学习如何使用 C# 和 `ASP.NET` 实现该模型。

## 静态页面

构成 Web 应用程序的文件以 `.htm`、`.html`、`.jsp`、`.php`、`.asp`、`.aspx`、`.asmx` 等扩展名结尾，或者可能是图像、视频、音乐或数据文件。Web 应用程序页面通常被分类为静态或动态。静态页面不需要在客户端计算机或 Web 服务器上进行任何处理。它们是预先创建的，位于服务器的硬盘上，并且基本上作为 `HTML` 或 `XHTML` 文档交付。`HTML` 文件包含格式化标记标签，这些标签会被 Microsoft Internet Explorer 等浏览器软件转换（渲染）为显示的图像。图 15–1 显示了在 Internet Explorer 中打开的静态 HTML 文档。如浏览器软件地址栏所示，该文件名称的一部分以 `.htm` 扩展名结尾。
