

# 使用 C# 进行 SQL Server 数据库编程

| 事件 | 描述 |
| :--- | :--- |
| ColumnChanged | 当 DataRow 中指定的 DataColumn 值发生更改后发生。 |
| ColumnChanging | 当 DataRow 中指定的 DataColumn 的值正在发生更改时发生。 |
| Disposed | 为组件的 Disposed 事件添加事件处理程序。 |
| InitializingDataTable | 在 DataTable 初始化后发生。 |
| RowChanged | 在 DataRow 成功更改后发生。 |
| RowChanging | 当 DataRow 发生更改时发生。 |
| RowDeleted | 在表中的某行被删除后发生。 |
| RowDeleting | 在表中的某行即将被删除之前发生。 |
| TableCleared | 在 DataTable 清空后发生。 |
| TableNewRow | 当插入新的 DataTable 时发生。 |

图 3.38 DataTable 的公共事件。

```csharp
// 创建一个新的 DataTable
DataTable FacultyTable = new DataTable("FacultyTable");

// 声明 DataColumn 和 DataRow 变量
DataColumn column;
DataRow row;

// 创建 DataColumn，设置类型、名称并添加到 DataTable 对象
column = new DataColumn();
column.DataType = Type.GetType("System.int32");
column.Name = "FacultyId";
FacultyTable.Columns.Add(column);

// 创建另一列。
column = new DataColumn();
column.DataType = Type.GetType("System.string");
column.Name = "FacultyOffice";
FacultyTable.Columns.Add(column);

// 创建 DataRow 对象并添加到 DataTable。
int i = 0;
for (int Index = 1; Index <= 10; Index++) {
    row = FacultyTable.NewRow();
    row("FacultyId") = Index;
    row("FacultyOffice") = "FC-" + Index;
    FacultyTable.Rows.Add(row);
}
```

图 3.39 创建新表并向表中添加数据的示例。

在结束本节之前，我们需要讨论如何创建一个表并向该新表添加列和行。图 3.39 显示创建一个新的数据表对象并向该 **FacultyTable** 表中添加列和行的示例。

参考图 3.39，从步骤 A 开始，创建了一个新的数据表实例 FacultyTable，并将其初始化为空表。
为了向此新表添加添加数据，你需要使用 Columns 和 Rows 集合，以及这两个集合的 **DataColumn** 和 **DataRow** 对象。因此，接下来你需要分别创建 **DataColumn** 和 **DataRow** 对象。步骤 F 完成了这些对象的声明。
在步骤 C 中，使用 **new** 关键字创建了 DataColumn 的新实例 **column**。使用两个 DataColumn 属性 **DataType** 和 **ColumnName** 来初始化第一个 DataColumn 对象，分别将数据类型设置为整数（System.int32），列名设置为“FacultyId”。完成后的 DataColumn 对象通过 Columns 集合的 `Add()` 方法添加到 FacultyTable 中。

在步骤 D 中，以与处理第一个数据列 *FacultyId* 相似的方式，将数据类型为字符串（System.string）且列名为“FacultyOffice”的第二列添加到 FacultyTable 中。

在步骤 E 中，使用 `for()` 循环来简化向 **FacultyTable** 中添加新行的过程。首先创建了一个循环计数器 Index，并通过 DataTable 的方法--`NewRow()` 创建了一个新的 DataRow 实例。总而言，我们向这个 FacultyTable 创建并添加了 10 行。对于第一列 FacultyId，循环计数器 Index 被分配给每一行。但对于第二列 FacultyOffice，则是建筑名称与循环计数器 Index 相结合。最后，在步骤 F 中，使用属于 Rows 类的 `Add()` 方法将 DataRow 对象 *row* 添加到此 FacultyTable 中。

当这段代码运行时，可以获得一个完整的 *FacultyTable*，它应该与图 3.40 中的表相一致。

# ADO.NET 简介

| FacultyId | FacultyOffice |
| :--- | :--- |
| 1 | TC-1 |
| 2 | TC-2 |
| 3 | TC-3 |
| 4 | TC-4 |
| 5 | TC-5 |
| 6 | TC-6 |
| 7 | TC-7 |
| 8 | TC-8 |
| 9 | TC-9 |
| 10 | TC-10 |

**图 3.40** 完成的 FacultyTable。

# 3.4.8 ADO.NET 4.3 ENTITY FRAME

大多数数据库（如 Microsoft Access、SQL Server 和 Oracle）都使用数据关系模型。但今天几乎所有的编程语言都是面向对象的语言，而数据结构的面向对象模型在这些这些语言的现代程序中广泛实现。因此，在当今现实世界中，数据库的关系模型与编程的面向对象模型之间存在潜在的冲突。尽管 ADO.NET 2.0 添加了一些新组件来解决这种冲突，但这并没有提供完全的解决方案。

ADO.NET 的最新版本是 4.3，但其关键问题之一与 ADO.NET 3.5 中的问题密切相关。随着 .NET Framework 3.0 发布 ADO.NET 3.5，针对该问题产生了一个革命性的解决方案。主要贡献包括在 ADO.NET 3.5 中添加了一些新组件：ADO.NET 3.5 Entity Framework（ADO.NET 3 EF）和 ADO.NET 3 Entity Data Model Tools。有了这些新组件，数据库的关系模型与面向对象编程项目之间的冲突可以得到完全解决。

ADO.NET 3.5 EF 的主要目标是提高数据编程的抽象级别，简化数据感知应用程序的开发并允许开发者编写更少的代码。Entity Framework 是 ADO.NET 的演变，允许开发者根据标准的 ADO.NET 3.5 抽象或持久化对象（ORM）进行编程，并构建在标准的 ADO.NET 3.5 提供模型之上，该模型允许访问第三方数据库。Entity Framework 引入了围绕实体数据模型（EDM）的新系列服务。

ADO.NET 3.5 提供了一个抽象数据库结构，将传统的逻辑结构转换为抽象或对象结构，分为三层：

- 概念层（Conceptual layer）
- 映射层（Mapping layer）
- 逻辑层（Logical layer）

ADO.NET 3.5 EF 使用一组 XML 文件定义了这三层，这些 XML 文件提供了抽象级别，使用户能够针对面向对象的概念模型进行编程，而不是关系数据模型。

概念层提供了一种允许开发者构建数据库面向对象访问的方法，数据库中的每个元素都可以被视为一个对象或实体。概念架构定义语言（CSDL）在这些 XML文件中定义实体和关系，这些关系将被映射层识别并使用，以建立实体与关系数据之间的映射。映射层使用映射架构语言（MSL）建立概念层中的实体与逻辑层中关系数据结构之间的映射。关系型数据库架构在逻辑层中使用存储定义语言（SSDL）定义在 XML 文件中。映射层充当桥梁或转换器，连接概念层的面向对象数据模型与逻辑层的关系数据模型。这种映射如图 3.41 所示，允许用户针对概念层编码并将这些代码映射到逻辑层。

概念层提供了一个实用的数据组件使用户开发面向对象的代码，称为实体（Entity）。本质上，客户端是一个带有相关组件的数据提供程序，如连接（EntityConnection）、命令（SqlCommand）和数据读取器（DataReader）。客户端与我们在本章前面的节讨论的其他提供程序类似，但它包含了新的组件和功能。

ADO.NET 3.5 EF 的核心是其实体数据模型（EDM），用户可以使用 ADO.NET 3.5 实体数据模型工具访问并使用该模型，这些工具包括实体数据模型项、实体数据模型向导、实体设计器、实体映射详情以及实体模型浏览器。

**图 3.41** 三层之间的映射关系。

