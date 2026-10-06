

# 30 第 2 章 介绍 LINQ to Objects

```csharp
11      );
12
13 // LINQ 扩展方法语法，与上述相同
14 var query2 = Person.SampleData(
15     .Where(c => c.State == "WA")
16     .Select(c => new
17     {
18         Name = c.FirstName + " " + c.LastName,
19         State = c.State
20     }));
21
22 foreach (var item in query1)
23     Console.WriteLine("{0}, {1}", item.Name, item.State);
```查询语法的详细解释将在第 3 章给出；其目的是演示语言特性如何为构建强大的查询语言系统奠定基础，正如其名称所示——集成语言的查询（Language Integrated Query）。

# LINQ to Objects 五分钟概述

LINQ to Objects 允许 .NET 开发人员对对象集合编写“查询”。微软提供了一大套内置查询操作符，这些操作提供的功能深度与任何处理关系型数据库的 SQL 语言的预期相当。

传统上，处理对象集合意味着编写使用 `for` 循环或 `foreach` 循环的列表代码来遍历集合，使用 `if` 语句进行过滤，同时执行其他计算（如对总属性进行累计求和）。

LINQ 将你从编写循环代码中解放出来；它允许你编写查询来过滤列表或对内存集合中的元素计算聚合函数，此外还有许多其他功能。你可以针对实现了 `IEnumerable<T>` 接口的任何集合类型编写查询，NET Framework 类提供的大多数内置集合类都实现了该接口，包括数组。

为了理解基本的查询语法，列表 2-8 和 2-9 展示了简单的 LINQ to Object 查询，其相应的控制台输出位于输出 2-3 和 2-4 中。

# 列表 2-8 整数数组的简单 LINQ 查询——参见输出 2-3

```csharp
int[] nums = new int[] { 0, 4, 2, 6, 3, 8, 3, 1 };

var result = from n in nums
    where n < 5
    orderby n
    select n;

foreach (int i in result)
    Console.WriteLine(i);
```

# 输出 2-3

```
0
1
2
3
4
```

# 列表 2-9 计算整数数组中所有值之的简单 LINQ——参见输出 2-4

```csharp
int[] nums = new int[] { 0, 4, 2, 6, 3, 8, 3, 1 };
int result = nums.Sum();
Console.WriteLine(result);
```

# 输出 2-4

> LINQ to Objects 扩展了任何继承自 `IEnumerable<T>` 的类型（使用上述的扩展方法），引入了一组与 SQL 语言类似的查询操作。.NET 基类库中内置的所有集合类型和数组都实现了 `IEnumerable<T>` 接口，因此通过一组扩展方法，微软为所有集合添加了查询能力。上一章的表 1-1 列出了内置查询操作符。本书稍后将将详细介绍每个操作符（第 3 到第 6 章）。如果你曾经处理过关系型数据库并编写过 SQL 查询，那么大多数操作符你应该是熟悉的。编写 SQL 查询和 LINQ 查询之间的一个重要区别是操作符顺序是反的。如果你习惯了 `Select-From-Where-OrderBy`，可能需要一些时间来克服肌肉记忆并转向 `From-Where-OrderBy-Select`。关键字顺序的差异有其道理，尽管 VB.Net 最初按照 SQL 顺序实现了 LINQ，但在意识到 IntelliSense 支持的益处后，切换到了 C# 的关键字顺序。先指定集合（使用 `from` 子句）允许 Visual Studio 在输入 `where` 和 `select` 子句时，在非常强大的工具提示中弹出公共字段和属性，如图 2-1 所示。如果先写 `select`，则无法提供弹出辅助，因为编辑器不知道整个查询中将使用何种对象类型。

```csharp
List<Contact> contacts = Contact.SampleData();
var q = from c in contacts
      select c;
```

| DateOfBirth |
| --- |
| Email |
| Equals |
| FirstName |
| GetHashCode |
| GetType |
| LastName |
| Phone |
| State |
| ToString |

图 2-1 通过指定 `from` 子句，编辑器可以在指定 `select` 子句时提供字段列表。如果 `select` 子句先出现，这是无法可能的。

为了演示 LINQ 的某些查询能力，概述的其余部分将使用表 2-1 和 2-2 所示的示例数据。本章及后续章节中的示例将以各种方式查询这些数据，以详细探索 LINQ to Objects。

# LINQ to Objects 五分钟概述

**表 2-1** 本书后续示例联系数据

| First Name | Last Name | D.O.B. | Phone | State |
|---|---|---|---|---|
| Barney | Gotshall | 19-Oct-1945 | 885 983 8858 | CA |
| Armando | Valdes | 9-Dec-1973 | 848 553 5487 | WA |
| Adam | Gauain | 3-Oct-1959 | 115 999 1154 | AK |
| Jeffery | Deane | 16-Dec-1950 | 677 602 6774 | CA |
| Collin | Zeeman | 10-Feb-1935 | 603 303 6030 | FL |
| Stewart | Kagel | 20-Feb-1950 | 546 607 5462 | WA |
| Chance | Lard | 21-Oct-1951 | 278 918 2789 | WA |
| Blaine | Reifsteck | 18-May-1946 | 715 920 7157 | TX |
| Mack | Kamph | 17-Sep-1977 | 364 202 3644 | TX |
| Ariel | Hazelgrove | 23-May-1922 | 165 732 165 | |

**表 2-2** 本书后续示例通话数据

| Number | Duration (mins) | Incoming | Date |
|---|---|---|---|
| 885 983 8858 | 5 | TRUE | 19-Oct-1945 |
| 848 553 5487 | 6 | TRUE | 9-Dec-1973 |
| 115 999 1154 | 7 | FALSE | 3-Oct-1959 |
| 677 602 6774 | 8 | TRUE | 16-Dec-1950 |
| 603 303 6030 | 9 | FALSE | 10-Feb-1935 |
| 546 607 5462 | 10 | TRUE | 20-Feb-1950 |
| 278 918 2789 | 12 | FALSE | 21-Oct-1951 |
| 715 920 7157 | 13 | TRUE | 18-May-1946 |
| 364 202 3644 | 14 | FALSE | 17-Sep-1977 |
| 165 732 165 | 15 | TRUE | 23-May-1922 |

