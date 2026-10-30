

## CHAPTER 3
## Windows 数据库应用程序

完成本章后，你将能够 ...

+   1. 从 Windows 窗体检索并显示 SQL Server 数据库中的数据。
+   2. 使用 ADO.NET 数据组件：TableAdapters、DataSets 和 DataConnectors。
+   3. 在网格和详细信息视图中显示数据库字段。
+   4. 使用方法和 SQL 查询对数据库数据进行排序。
+   5. 使用 SQL 或 DataSet 设计器连接数据字段。
+   6. 使用存储过程访问数据。
+   7. 编写多层应用程序，将数据层与表示层分离。
+   8. 在代码中声明并实例化 DataSet 和 TableAdapter 对象，并编写将数据绑定到窗体控件的代码。

在本章中，你将学习如何在 Windows 窗体上访问和显示数据库数据。你将遵循良好的 OOP 原则，并在数据层组件中执行数据库访问。你将学习使用表适配器和 DataSets 从数据库文件显示数据。本章将介绍检索数据的底层 SQL 语句，并介绍存储过程。在第 4 章中，你将处理多个相关表，在第 5 章中你将学习更新数据库。

### Visual Studio 和数据库应用程序

专业的 VB 程序员将大部分时间花在涉及数据库的应用程序上。要成为一名优秀的程序员，你需要专注于显示和更新数据库信息的各种方法。

使用 VB，你可以创建几乎不需要编码的非常简单的数据库应用程序，一直到可以访问和修改多个大型服务器上的数据的非常强大的分布式应用程序。你可以创建在单台独立计算机上显示和/或更新数据的程序，以及多用户网络数据库。尽管本文主要集中在 SQL Server Express 数据库上，但你所学习的技术也扩展到更大规模的数据库，如 SQL Server、Oracle、Sybase 和 DB2。你也可以将本章中的大多数技术应用于 Access 数据库。

随 .NET Framework 一起提供的托管提供程序是

+   - Microsoft Access 数据库文件。
+   - Microsoft ODBC 数据源。
+   - Microsoft SQL Server Compact 3.5。
+   - Microsoft SQL Server 数据库文件。
+   - Oracle 数据库（其他数据库格式）。

### ADO.NET

ActiveX Data Objects (ADO) .NET 3.5 是微软最新的数据库对象模型。ADO.NET 的目标是允许程序员使用一组标准对象来引用来自任何来源的数据。

访问来自 Web 和多个平台的数据的趋势改变了我们用于数据处理的技术。过去，通常以客户端/服务器格式连接到数据库。连接在用户浏览和/或更新数据时保持打开状态，数据类型并不是太大的问题。但现在，使用 .NET 方法，我们使用断开连接的 DataSets，具有来自多个来源的通用数据表示（数据类型）。.NET Framework 也与可扩展标记语言（XML）紧密集成，XML 是在多个平台上存储和传输数据的行业标准格式。

### 在 .NET Framework 中访问数据

你会发现用于处理数据的全新术语：数据源、数据设计器、数据集、绑定源、表适配器等。此外，你还将使用数据元素的许多标准术语。

### 数据库术语

数据表可以像电子表格一样查看——具有行和列。表中的每一行代表一个项目、人员或交易的数据，称为记录。表中的每一列用于存储不同的数据元素，例如账号、姓名、地址或数字金额。列中表示的元素称为字段。你可以将图 3.1 中的表视为由行和列或记录和字段组成。

一个表由行（记录）和列（字段）组成。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_130_0.png)

大多数表使用主键字段（或字段组合）唯一标识每条记录。主键字段通常是一个数字，例如员工编号、账号、识别号或社会安全号码；也可能是文本字段，例如姓氏，或组合，例如姓氏和名字。

### 数据源

你的应用程序从数据源获取数据。你可以从大型数据库、本地数据库文件、Web 服务或其他类型的对象创建数据源。对于驻留在开发人员计算机上的本地数据库文件，.NET 目前支持 Access .mdb 和 .accdb 文件以及 SQL Server Express .mdf 文件。SQL Server Express .mdf 文件是 Visual Basic 的推荐选择。Visual Studio 环境允许你创建和编辑 SQL Server Express 数据源。

当你从数据库创建数据源时，会向你的项目添加一个强类型 DataSet。每个强类型 DataSet 都有一个模式，描述字段及其数据类型。虽然 .NET 提供了几种类型的数据源，但我们将集中于强类型 DataSets，这是在大多数情况下处理数据的推荐方法。

### DataSet 对象

DataSet 对象在内存中保存数据的副本，与数据源断开连接。你可以将 DataSet 视为临时缓存，而不是实际的数据库数据。

DataSet 对象可以保存一个或多个表。关系数据库通常包含多个表以及表之间的关系。例如，Employee 表可能有 Employee ID 字段，Payroll 表也将有 Employee ID 字段。两个表通过 Employee ID 相关联。你可以通过检索对应 Employee ID 的记录来找到一条工资记录的员工信息。在图 3.2 的示例中，Employee ID 是 Employee 表的主键。Payroll 表中的 Employee ID 字段被视为外键——将 Payroll 记录链接到其对应 Employee 记录的字段。因此，例如，要检索给定 Payroll 记录的员工姓名，外键用于查找 Employee 表中对应的记录。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_131_0.png)

图 3.2
Employee 表和 Payroll 表通过 Employee ID 相关联，Employee ID 是 Employee 表的主键，也是 Payroll 表的外键。

### DataSet 对象模型

每个 DataSet 对象包含一个 DataTable 集合，由单独的 DataTable 对象组成。DataTable 对象同时具有 DataRow 和 DataColumn 集合。单个 DataRow 保存一条记录的实际数据。DataRow 对象维护原始值和任何更改的值。此信息用于确定程序执行期间哪些行已更改。

DataRelation 对象存储有关相关表的信息，包括哪些列包含链接表的键和外键。Constraints 集合属于 DataTable 对象，包含两种类型的 Constraint 对象：Unique 约束和 ForeignKey 约束。Unique 约束强制指定字段中的值唯一，这通常是主键字段的要求。ForeignKey 约束要求出现在二级表中的任何外键值都必须与主表中的主键值匹配。

图 3.3 显示了 DataSet 对象的对象模型。
注意：请参阅 Visual Studio 帮助中的“Visual Studio 中的数据集概述”。

### TableAdapters

TableAdapter 对象提供程序与数据库之间的通信，有时称为“数据访问层”。TableAdapter 连接到数据库并处理 SQL 查询和存储过程，填充 DataSets，并处理将任何更改写回数据源。

TableAdapter 的一个特性是它可以保存多个查询。你可以通过调用特定查询或获取表的全部数据来检索数据。这些 TableAdapter 对象比本教材早期版本中使用的 DataAdapters 功能更强大。（DataAdapters 在 VB 2008 中仍然可用。）Visual Studio IDE 中的可视化设计器在你添加强类型 DataSet 时会自动为你生成 TableAdapters。

