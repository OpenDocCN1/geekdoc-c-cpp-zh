
b. `Connection`

c. `DataReader`

d. `Command`

- 8. `DataReader` 是一个只读类，它只能用于在执行 ______ 方法时检索并持有从数据库返回的数据行。

  a. `Fill`

  b. `ExecuteNonQuery`

  c. `ExecuteReader`

  d. `ExecuteQuery`

- 9. 在退出项目之前，需要使用 ______ 方法释放所有用于数据驱动应用程序的对象。

  a. `Release`

  b. `Nothing`

  c. `Clear`

  d. `Dispose`

- 10. 为了在 `DataSet` 和数据库之间 ______ 数据，应该使用 ______ 对象。

  a. `Bind`, `BindingSource`

  b. `Add`, `TableAdapter`

  c. `Move`, `TableAdapter`

  d. `Remove`, `DataReader`

# III. 练习题

- 1. 解释 `ADO.NET` 2.0 的两种架构，并使用基本组件的框图阐述这两种架构的功能。

- 2. 列出 `ADO.NET` 2.0 的三个基本组件，以及数据提供程序的不同版本及其子组件。

- 3. 用示例说明 `Command` 对象属性的 `Command` 和参数集合（`Parameter collection`）之间的关系。阐述如何向 `Parameters` 集合添加参数。假设使用了带有两个参数的 `SQL Server` 数据提供程序：参数名 `parameter_name`: `username`, `password`，参数值 `parameter_value`: `Name`, `Come`。

# ADO.NET 简介

- 4. 解释 `DataSet` 和 `DataTable` 之间的关系。阐述如何使用 `Fill` 方法来填充 `DataSet`。假设数据查询字符串是一个 `SQL SELECT` 语句：`SELECT faculty_id, faculty_name FROM Faculty`，并且使用了 `SQL Server` 数据提供程序。

- 5. 解释 `ADO.NET` 3.5 实体框架 (`EF`) 和 `ADO.NET` 3.5 实体框架工具 (`EFT`) 的组件和功能。

- 6. 阐述 `ADO.NET` 3.5 实体数据模型与其关联组件（如项模板、向导和设计器）之间的关系。

- 7. 解释 `ADO.NET` 3.5 实体数据模型三层（概念层 `Conceptual`、映射层 `Mapping` 和逻辑层 `Logical layer`）之间的关系。

![](img/d59a47501d0a20fc0460a49c469c6fb7_132_0.png)

# 语言集成查询 (LINQ) 简介

语言集成查询 (`LINQ`) 是 `Visual Studio 2008` 和 `.NET Framework 3.5` 版本中的一项突破性创新，它桥起了对象世界与数据世界之间的鸿沟。

传统的，针对数据的查询以简单字符串的形式表示，在编译时没有类型检查，也没有 `IntelliSense` 支持。此外，你必须为每种数据源学习不同的语言：`Microsoft Access`、`SQL` 数据库、`XML` 文档、各种 `Web` 服务和 `Oracle` 数据库。`LINQ` 使查询成为 `C#` 和 `Visual Basic` 中的一等语言构造结构。你可以使用关键字和系列操作符对强类型对象集合编写查询。

在 `Visual Studio.NET` 中，你可以对 `SQL Server`、`XML` 文档、`ADO.NET DataSets` 以及任何支持 `IEnumerable` 或 `IEnumerable<T>` 接口的对象集合进行 `LINQ` 查询。如第 3 节所述，对 `ADO.NET 3.5` 实体框架的 `LINQ` 支持也已在计划中，并且第三方正在为许多 `Web` 服务和数据库实现编写 `LINQ` 提供程序。

你可以在新项目中使用 `LINQ` 查询，也可以在现有项目中与非 `LINQ` 查询并用。唯一的要求是该项目应该在 `.NET Framework 3.5` 环境下开发。

在我们深入研究 `LINQ` 之前，最好对 `LINQ` 有一个通用且全局的了解。让我们从 `LINQ` 的基础介绍开始。

## 4.1 语言集成查询概述

`LINQ` 模式建立在一组称为标准查询操作符 (`SQO`) 的方法的基础上。这些方法中的大部分在序列上操作，其中序列是一个其类型实现了 `IEnumerable<T>` 或 `IQuery<T>` 接口的对象。标准查询操作符提供了查询能力，包括过滤、投影、聚合、排序等。所有的 `SQO` 方法都位于 `System.Linq` 命名空间中。要使用这些方法，必须在代码窗口的命名空间部分使用指令声明此命名空间，例如：`System.Linq`。

存在可能引起混淆的符号和术语，例如 `IEnumerable`、`IEnumerable<T>`、`IQuery` 和 `IQuery<T>`。让我们先仔细查看这些术语。

### 4.1.1 LINQ 中用到的一些接口

四个接口 `IEnumerable`、`IEnumerable<T>`、`IQuery` 和 `IQuery<T>` 在通过 `SQO` 的 `LINQ` 查询中被广泛。事实上，有两个接口和 `IQuery` 主要用于 `C#` 早期版本（如 `C# 1.0`）支持的非泛型集合，另外两个 `IEnumerable<T>` 和 `IQuery<T>` 用于将 `C# 2.0` 中与 `System.Collection.Generic` 兼容的类型数据转换为 `IEnumerable<T>` (`LINQ to Objects`) 或 `IQuery<T>` (`LINQ to SQL`)，因为 `LINQ` 使用强类型集合进行查询。

# 语言集成查询 (LINQ)简介

```csharp
// create an Integer array
int[] myArray = new int[] {1, 2, 3, 4, 5 }; IEnumerable<int> query = from num in myArray
                    where num >= 3
                    select num;

foreach (var intResult in query)
{
    Console.WriteLine(intResult);
}
```

**图 4.2** 使用 `LINQ to object` 对象查询的编码示例修改。

通过完成这两项，应该清楚地看到 `IQueryable` 和 `IEnumerable<T>` 接口在 `LINQ to Objects` 查询中起着关键作用。前者用于非泛型集合，后者用于泛型集合。关键点在于，典型的 `LINQ to Objects` 表达式不仅接受实现 `IEnumerable<T>` 的类作为数据源，而且返回一个具有相同类型的实例。

### 4.1.1.2 IQueryable 和 IQueryable<T> 接口

如上一节所述，`IQueryable` 和 `IQueryable<T>` 是用于 `LINQ to SQL` 查询的两个接口。类似于 `IEnumerable` 和 `IQueryable<T>` 接口（其中标准查询操作方法被定义为 `Enumerable` 类中的静态成员），`IQueryable<T>` 接口的标准查询操作方法被定义为 `Queryable` 类的静态成员。`IQueryable` 接口主要用于非泛型集合，而 `IQueryable<T>` 用于泛型集合。另一点是 `IQueryable<T>` 接口继承自 `Queryable` 类中的 `IEnumerable<T>` 接口，其接口定义如下：

```csharp
interface IQueryable<T> : IEnumerable<T>, Queryable
```

通过这种继承，我们可以将 `IQueryable<T>` 序列视为 `IEnumerable<T>` 序列。图 4.3 显示了使用 `IQueryable` 接口对数据库 `CSE_DEPT` 进行查询的示例。在创建此代码之前，已使用 `DataContext` 对象建立了数据库。`Login` 是该数据库中的一个表名，它是

```csharp
// create a database connection using the DataContext object
public CSE_DEPTDataContext cse_dept = new CSE_DEPTDataContext();
// create local variables
string username = string.Empty;
string password = string.Empty;
// LINQ query expression
IQueryable<Login> login = from lg in cse_dept.Logins
                            where lg.user_name == txtUserName.Text &&
                            lg.pass_word == txtPassWord.Text
                            select lg;

foreach (log in login)
{
    username = log.user_name;
    password = log.pass_word;
}
```

**图 4.3** 使用 `LINQ to SQL` 查询的编码示例。

被 `LINQ` 查询操作转换为实体，一个 `IQueryable<T>` 接口（确切说是标准查询操作）被用于执行此操作。`Login` 在 `IQueryable<T>` 接口中作为类型类型工作，以确保输入和返回的序列都是 `Login` 类型的强类型序列。标准查询操作获取并返回匹配的序列，并使用 `foreach` 循环将它们分配给相关的字符串变量。现在让我们来看标准查询操作 (`SQO`)。

## 4.1.2 标准查询操作

`LINQ` 标准查询操作分为两组，一组作用于 `IEnumerable<T>` 类型的对象，另一组作用于其他类型。构成每组的方法分别是 `Enumerable` 和 `Queryable` 类的静态成员。它们被定义为其所操作类型的扩展方法。这意味着它们可以通过静态语法或实例方法调用。

此外，标准查询操作方法还作用于基于 `IEnumerable<T>` 或 `IQueryable<T>` 以外的类型。`Enumerable` 类型定义了两个作用于 `IEnumerable` 类型对象的方法。这两个方法 `Cast<T>(IEnumerable)` 和 `Type<T>(IEnumerable)` 允许你以 `LINQ` 模式查询非参数或非泛型集合。它们通过创建强类型对象集合来实现。`Queryable` 类定义了两个类似的方法 `Cast<T>(IQueryable)` 和 `Type<T>(IQueryable)`，它们作用于 `Queryable` 类型的对象。

标准查询操作的区别在于它们的执行方式，取决于它们返回的是单个值还是值值序列。返回单个值的方法（例如 `Average` 和 `Sum`）立即执行。返回序列的方法则延迟执行并返回一个可枚举对象。

对于操作内存中集合的方法（即那些扩展 `IEnumerable<T>` 的方法），返回的可枚举对象捕获了传递给方法的参数。当对象被执行时，将采用查询操作的逻辑并返回结果。

此相反，扩展 `IQueryable<T>` 方法不实现任何查询行为，而是构建一个表示要执行的查询的表达式树。查询处理由源 `IQueryable<T>` 对象处理。

方法的调用可以在一个查询中链式，使得查询可以变得任意复杂。

根据功能，标准查询操作和非延迟标准查询操作可以分为两类：延迟标准查询操作和立即执行标准查询操作。图 4.4 列出了一些最常用的标准查询操作。

由于作用范围限制，我们将选择一些常用的标准查询操作并逐一对它们进行详细讨论。

## 4.1.3 延迟标准查询操作

延迟查询操作和非延迟操作都是根据其目的组织的，我们将根据其目的对其进行讨论。

### AsEnumerable（转换目的）

`AsEnumerable` 方法除了将实现 `IEnumerable<T>` 的源的编译时类型更改为 `IEnumerable<T>` 之外，没有其他影响。这意味着，如果输入序列的类型为 `IEnumerable`，则输出序列也将转换为具有相同类型的序列。`Enumerable`。

### Cast（转换目的）

# 语言集成查询 (LINQ)简介

| 标准查询操作 | 目的 | 延迟 |
|---|---|---|
| All | 量化 | 否 |
| Any | 量化 | 否 |
| AsEnumerable | 转换 | 是 |
| Average | 聚合 | 否 |
| Cast | 转换 | 是 |
| Distinct | 集合 | 是 |
| ElementAt | 元素 | 否 |
| First | 元素 | 否 |
| Join | 链接 | 是 |
| Last | 元素 | 否 |
| OType | 转换 | 是 |
| OrderBy | 排序 | 是 |
| Select | 投影 | 是 |
| Single | 元素 | 否 |
| Sum | 聚合 | 否 |
| ToArray | 转换 | 否 |
| ToList | 转换 | 否 |
| Where | 限制 | 是 |

图 4.4 最常用的查询操作。

```csharp
FacultyDataAdapter.SelectCommand = accCommand;
FacultyDataAdapter.Fill(ds, "Faculty");
var facultyinfo = (from fi in ds.Tables("Faculty").AsEnumerable()
    where fi.Field<string>("faculty_name").Equals(ComboName.Text))
foreach (var row in facultyinfo)
{
//Display selected row elements...
}
```

图 4.5 `AsEnumerable` 运算符的示例代码。

此查询结构的关键点是 `AsEnumerable()` 运算符。由于不同的数据库系统使用不同的集合和查询操作，必须将它们转换为 `IEnumerable<T>` 类型，以便使用标准查询操作在 `LINQ` 中对 `IEnumerable<T>` 序列执行复杂的数据查询。如果没有此运算符，将遇到编译错误。

### Join（链接目的）

两个数据源的连接是将一个数据源中的对象与另一个数据源中具有共同属性的对象关联起来。连接是对于彼此关系无法直接遵循的查询的重要操作。在面向对象的编程中，这可能意味着对象之间存在未建模的关联，例如反向的

# 使用 C# 进行 SQL Server 数据库编程

```csharp
System.Collections.ArrayList fruits = new System.Collections.ArrayList();
fruits.Add("apple");
fruits.Add("mango");

IEnumerable<string> query = fruits.Cast<string>().Select(fruit => fruit);
foreach (string fruit in query) {
    Console.WriteLine(fruit);
}
```

// 这段代码的运行结果是：

- apple

- mango

图 4.6 `cast` 操作符示例代码。

单向关系。单向关系的一个示例是 `Customer` 类，它拥有一个类型为 `City` 的属性，而 `City` 类没有作为 `Customer` 对象集合的属性。如果你有一个 `City` 对象列表并想要找到每个城市的所有客户，可以使用连接（`join`）操作来查找它们。

`LINQ` 框架提供的方法是 `Join` 和 `GroupJoin`。这些方法执行等值连接，即根据键的相等性匹配两个数据源的连接。在关系数据库术语中，`Join`实现了内连接（`inner join`），它是连接的一种类型，只返回在另一个数据源中有匹配项的对象。`GroupJoin` 方法在关系数据库术语中没有直接对应项，但它是内连接和外连接的超集。左外连接（`Left outer join`）是返回第一个（左）数据源每个元素的连接，即使它在另一个数据源中没有关联元素。

图 4.7 显示了使用该操作符的示例。我们需要根据 `faculty_name` 从 `Course` 表中查询所选教职人员的所有课程 (`course_id`)。问题在于，`Course` 表中没有 `faculty_name` 列，只有 `faculty_id` 与相关的 `course_id` 关联。因此，我们必须首先根据 `faculty_name` 从 `Faculty` 表获取 `faculty_id`，然后从 `Course` 表中查询 `course_id`。这个问题可以通过图 4.7 所示的连接操作符方法得到有效解决。

### 类型（转换目的）

该方法使用延迟执行实现。立即返回的值是一个包含执行该操作所需的所有信息的对象。该方法表示的查询在通过调用 `GetEnumerator` 方法或在 `Visual C#` 中使用 `foreach` 对对象进行枚举之前是不会执行的。

```csharp
var courseinfo = Courses
    .Join(Faculty, ci => ci.faculty_id, o => o.faculty_id)
    .Where(fi => fi.faculty_name == ComboName.Text)
    .Select(new {
        course_id = ci.course_id
    });
foreach (var cid in courseinfo) {
    CourseList.Items.Add(cid.course_id);
}
```

图 4.7 `Join` 操作符示例代码。

# 集合集成查询 (LINQ) 简介
