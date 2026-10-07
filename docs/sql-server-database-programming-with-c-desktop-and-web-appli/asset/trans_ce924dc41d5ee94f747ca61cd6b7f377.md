

# 语言集成查询 (LINQ) 简介

Entity Framework 和 LINQ 均可以使用。以下是创建和执行 LINQ to Entities 查询的过程：

- 1) 从 `ObjectContext` 构建一个 `ObjectQuery` 实例。
- 2) 使用 `ObjectQuery` 实例在 C# 中编写 LINQ to Entities 查询。
- 3) 查询中的 LINQ 标准查询运算符和表达式被转换为命令树（command tree）。
- 4) 以命令树形式表示的查询针对数据存储执行。执行过程中数据存储上抛出的任何异常将直接传递给客户端。
- 5) 查询结果被实例化（materialized）到客户端。

让我们对这些步骤每一个进行更详细的讨论。

## 4.7.4.1 构建 ObjectQuery 实例

`ObjectQuery` 泛型类表示返回零或多个类型化实体的查询。每个对象查询通常从现有的对象上下文（object context）中构建，而不是手动构建，并且始终属于该上下文。该上下文提供了构建和执行查询所需的连接和元数据。`ObjectQuery` 泛型类实现了 `IQueryable` 泛型接口，其构建方法允许 LINQ 查询能够增量构建。

## 4.7.4.2 编写 LINQ to Entities 查询

实现 `IQueryable` 接口的查询泛型类实例作为 LINQ to Entities 查询的数据源。在查询中，你精确指定了想要从数据源检索的信息。查询还可以在执行前指定应如何对信息进行排序、分组和成型处理。在 LINQ 中，查询存储在变量中。查询不接受参数也不返回数据；它只存储查询信息。在创建查询后，你必须执行它以检索数据。

LINQ to Entities 查询可以使用两种不同的语法编写：查询表达式语法（query expression syntax）和基于方法的查询语法（method-based query syntax）。我们在本章的第 4.5.1.1 和 4.5.1.2 节中提供了关于查询表达式语法和基于方法查询语法的详细讨论，并配有真实的代码示例。请参考这些内容以清晰了解这两种语法。

## 4.7.4.3 将查询转换为命令树

为了针对 Entity Framework 执行 LINQ to Entities 查询，必须将 LINQ 查询转换为针对 Entity Framework 执行的命令树表示形式。

LINQ to Entities 查询由 LINQ 标准查询运算符（如 `Select`、`Order` 和 `OrderBy`）和表达式组成。LINQ 标准查询运算符不是类类，而是类上的静态方法。在 LINQ 中，表达式可以包含任何使用 `System.Expressions` 命名空间内类型的内容，扩展而言之，包含任何可以用 lambda 表达式表示的内容。这是 Entity Framework 允许的表达式的超集，而根据定义，Entity Framework 的表达式受限于数据库允许且由 `ObjectQuery` 支持的操作。

在 Entity Framework 中，运算符和表达式都由单一层级结构表示。Entity Framework 使用命令树来执行查询。如果 LINQ 查询无法表示为命令树，则在转换时将抛出异常。LINQ to Entities 的转换涉及两个子转换：标准查询运算符的转换和表达式的转换。通常情况下，LINQ to Entities 中的表达式在服务器上评估，因此不应期望表达式遵循 CLR 语义。

图 4.42 显示了 LINQ to Entities 中使用的表达式示例。

# 152 使用 C# 进行 SQL Server 数据库编程

```c
IQueryable<string> FacultyInfo = from fi in Faculties
where fi.faculty_id == "B788880"
select fi.faculty_name;
```

**图 4.42** 使用 LINQ to entities 的表达式示例。

## 4.7.4.4 执行查询

在用户创建 LINQ 查询后，它会被转换为与 Entity Framework 兼容的表示形式（命令树形式），然后针对数据存储进行执行。在查询执行时，所有查询（或查询的组件）都会在客户端或服务器上进行评估。这包括在结果实例化或投影示例中使用的表达式。

查询表达式可以通过两种方式执行。LINQ 查询在变量每次被迭代时执行，而不是在创建查询变量时执行；这被称为**延迟执行**（deferred execution）。也可以强制查询立即执行，这对于缓存结果非常有用。图 4.43 所示的示例使用 `Select` 返回来自 *Faculty* 的所有行并显示院系名称。在 *foreach* 循环中迭代查询变量会触发查询执行。

当执行 LINQ to Entities 查询时，查询中的某些表达式必须在客户端执行，且在服务器上执行查询之前执行某些部分。表达式的客户端评估在客户端进行，其评估结果将替换查询中的表达式，然后在服务器上执行查询。由于查询是在数据存储上执行的，数据存储的配置将覆盖客户端指定的行为。空值处理和数值精度就是此类示例。服务器上查询执行期间的任何异常将直接向上传递给客户端。

## 4.7.4.5 查询实例化

实例化（Materialization）是将数据返回给 CLR 的过程。LINQ to Entities 的实例化通常由 Entity Framework 完成，返回以下内容之一：

- 零或多个类型化实体的集合
- 匿名类型。
- 分组实例。

```csharp
ObjectQuery<Faculty> faculties = from fi in Faculties
where fi.faculty_id == "B788880"
select fi.faculty_name;

Console.WriteLine("Faculty Names:");
foreach (var name in faculties)
{
    Console.WriteLine(name);
}
```

**图 4.43** 执行查询的示例。

# 语言集成查询 (LINQ) 简介

153

![](img/d5947501d0a20fc0460a49c6fb7181_0.png)

图 4.44 LINQ to entities 的简化结构。

- 内联集合。
- 匿名类型。
- 分组实例。
- Queryable 实例。

## 4.7.5 LINQ to Entities 的实现

为了使用 LINQ to Entities 对数据库执行操作，需要对基础设施有清晰的认识，并完全理解 LINQ to Entities 使用的所有组件。在第 3 章的第 3.4-8 节中，我们提供了 ADO.NET 3.5 Entity Framework 和 ADO.NET 3.5 Entity Data 的详细讨论，使用了实体模型向导、实体模型设计器和实体模型浏览器。查看该章节以获取有关 LINQ to Entities 实现的更多细节。使用 LINQ to Entities 查询的完整项目 EDModelProject 可以在 CRC Press 网站的 Students 文件夹下的 Class Projects Chapter 3 中找到（参考图 1）。

## 4.8 LINQ to XML

LINQ to XML 的开发是考虑到 XML 的语言集成查询的，它利用了标准查询运算符并添加了针对 XML 的查询扩展。LINQ to XML 是一种现代的内存 XML 编程语言，利用了最新的 .NET Framework 创新。它在不同的 LINQ 启用数据技术中提供了一致的 DOM 和 XQuery/XPath 类似的功能。

