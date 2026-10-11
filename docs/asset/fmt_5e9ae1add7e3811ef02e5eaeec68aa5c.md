
由于对象初始化语法具有类似的目标，集合初始化被赋予了类似的功能，类似于常见的“构造并添加”模式。集合必须实现 `System.Collections.IEnumerable` 并具有 `Add` 方法的适当重载以支持新的初始化语法。列表 2-3 展示了新集合初始化语法的用法，并显示了对应的对等代码模式。它还演示了如何将集合初始化与对象初始化相结合，这有助于保持代码更整洁且通常更容易阅读。

### 列表 2-3 集合初始化语法——修改前后

```csharp
// 旧的初始化语法 => 多条语句
List<string> stringsOld = new List<string>();
stringsOld.Add("string 1");
stringsOld.Add("string 2");

// 新的初始化语法 => 单条语句
List<string> stringsNew = new List<string> {
    "string 1",
    "string 2"
};

// 结合对象和集合初始化
// 创建联系人列表并添加两条记录。
List<Contact> list = new List<Contact> {
    new Contact {
        LastName = "Magennis",
        DateOfBirth = new DateTime(1973, 12, 09)
    },
    new Contact {
        LastName = "Doherty",
        DateOfBirth = new DateTime(1978, 1, 05)
    }
};
```

## 隐式类型变量

当使用 `var` 关键字而不是具体类型时，类型从初始化值推推出来。隐式类型变量是强类型的；列表 2-4 展示了隐式类型变量的用法。

### 列表 2-4 隐式类型变量

```csharp
// 隐式类型变量声明 => 多处声明
var anInt = 1;
var aString = "Testing";
var listContact = new List<Contact>();
var intArray = new int[] { 0, 1, 2, 3, 4 };

// 隐式类型变量声明 => 单条语句
// 它展示了对象和集合
// 初始化如何与 var 风格配合。
var list = new List<Contact> {
    new Contact {
        LastName = "Magennis",
        DateOfBirth = new DateTime(1973, 12, 09)
    },
    new Contact {
        LastName = "Doherty",
        DateOfBirth = new DateTime(1978, 1, 05)
    }
};
var intArray = new int[] { 0, 1, 2, 3, 4 };
```

## 匿名类型

匿名类型是编译时生成的类型，其属性在编译时从对象初始化表达式继承。这些类型随后可以作为临时存储类在方法内部使用，避免了为每组属性构建特定的数据类。新类直接继承自 `System.Object` 且没有名称（至少在代码中无法引用）。你为匿名类型分配什么运行时类型？它们必须使用前面提到的隐式类型局部变量结构 (`var`) 来声明。

匿名类型通过在 `new` 语句后省略类型名并提供包含一个或多个赋值的有效对象初始化表达式来定义。列表 2-5 展示了如何创建匿名类型以及如何在后续代码中使用它，其输出见输出 2-2。

### 列表 2-5 匿名类型的声明与使用——参见输出 2-2

```csharp
// 简单的匿名类型声明
Console.WriteLine("- Simple Anonymous Type -");
var item = new { Name = "Car", Price = 9989.00 };
```

```csharp
Console.WriteLine("Type: {0}, Name: {1}, Price: {2}",
item.GetType().ToString(), item.Name, item.Price);
```

### LINQ 启用 C# 3.0 语言增强 25

```csharp
// 声明并操作匿名类型数组
Console.WriteLine();
Console.WriteLine("- Iterating Anonymous Types Array -");
var list = new[] { {
    new { LastName = "Magennis",
         DateOfBirth = new DateTime(1973,12,09) },
    new { LastName = "Doherty",
         DateOfBirth = new DateTime(1978,1,5) }
};

foreach (var x in list) {
    Console.WriteLine("{0} ({1})*", x.LastName, x.DateOfBirth);
}
```

```csharp
// 编译器优化 - 选 C# 规范：
// 在同一个程序内，两个匿名对象初始化器
// 如果它们以相同的顺序指定了具有相同
// 名称和相同编译时类型的属性序列，
// 将将产生相同的匿名类型实例。
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2; // 有效：相同的匿名类型。
```

## 输出 2-2

- Simple Anonymous Type - 

Type: <>f__AnonymousType2<System.String,System.Double>,

Name: Car,

Price: 9989

- Iterating Anonymous Types Array - 

Magennis (12/9/1973 12:00:00 AM)

Doherty (1/5/1978 12:00:00 AM)

当编写使用现有类型的子集属性构建集合的查询（称为投影）时，匿名类型的重要性变得显而易见。想象一下在操作关系型数据库时，你无法定义用于 SQL 查询返回的列列表。LINQ 也存在同样的问题；如果没有匿名类型，你将为每一个更改了感兴趣列的返回集定义一个具体的类型。C# 4.0 中添加的可选参数（在第4章“数据的分组和连接”中介绍）使得这种情况稍微容易；当需要临时结果时应该考虑匿名类型。

除了支持 LINQ 的用处外，匿名类型还允许在处理数据期间创建临时数据结构。以前通常需要构建一个仅包含属性声明的普通类来支持数据存储；匿名类型完美地满足了这一需求。虽然通过将参数类型声明为 `Object`可以将匿名类型传递到声明它的方法之外，但这是非常不建议的。在 LINQ 功能之外使用匿名类型时，请将其范围限制在它们所在的方法中，否则请定义具体的类型或结构体。

## Lambda 表达式

Lambda 表达式基于 C# 2.0 添加的匿名方法功能构建。匿名方法添加了使用 `delegate` 关键字内联代码的能力，这提供了一种更简洁的方法编写方式。C# 3.0 引入的 Lambda 表达式通过使用 `=>` 运算符提供了更简洁的语法。Lambda 表达式由参数列表以及表达式或正体组成。这种语法允许省略 `delegate` 关键字和参数类型，因为编译器可以从上下文中推断出来。Lambda 表达式在 LINQ 查询定义过滤器和投影时特别有用。

虽然 Lambda 表达式可以单独使用，但它们经常被用作接收委托作为参数的方法的参数。这是 LINQ 方法（如 `Select`、`Where` 和 `OrderBy`）中的常见模式。通过使用 Lambda 表达式，与传统的匿名方法或单独的委托定义相比，代码变得更具读性和可维护性。

### 30 第 2 章 介绍 LINQ to Objects

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

## LINQ to Objects 五分钟概述

LINQ to Objects 允许 .NET 开发人员对对象集合编写“查询”。微软提供了一大套内置查询操作符，这些操作提供的功能深度与任何处理关系型数据库的 SQL 语言的预期相当。

传统上，处理对象集合意味着编写使用 `for` 循环或 `foreach` 循环的列表代码来遍历集合，使用 `if` 语句进行过滤，同时执行其他计算（如对总属性进行累计求和）。

LINQ 将你从编写循环代码中解放出来；它允许你编写查询来过滤列表或对内存集合中的元素计算聚合函数，此外还有许多其他功能。你可以针对实现了 `IEnumerable<T>` 接口的任何集合类型编写查询，NET Framework 类提供的大多数内置集合类都实现了该接口，包括数组。

为了理解基本的查询语法，列表 2-8 和 2-9 展示了简单的 LINQ to Object 查询，其相应的控制台输出位于输出 2-3 和 2-4 中。

## 列表 2-8 整数数组的简单 LINQ 查询——参见输出 2-3

```csharp
int[] nums = new int[] { 0, 4, 2, 6, 3, 8, 3, 1 };

var result = from n in nums
    where n < 5
    orderby n
    select n;

foreach (int i in result)
    Console.WriteLine(i);
```

## 输出 2-3

```
0
1
2
3
4
```

### 列表 2-9 计算整数数组中所有值之的简单 LINQ——参见输出 2-4

```csharp
int[] nums = new int[] { 0, 4, 2, 6, 3, 8, 3, 1 };
int result = nums.Sum();
Console.WriteLine(result);
```

## 输出 2-4

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

## LINQ to Objects 五分钟概述

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

## 列表 2-12 根据电话号码对两个集合进行查询——参见输出 2-7。

注意临时临时匿名类型的使用。

```csharp
List<Contact> contacts = Contact.SampleData();
List<CallLog> callLog = CallLog.SampleData();
```

```csharp
var q = from call in callLog
  join contact in contacts on
      call.Number equals contact.Phone
  select new {
      contact.FirstName,
      contact.LastName,
      call.When,
      call.Duration
  };

foreach (var c in q)
  Console.WriteLine(
      "{0} - {1} ({2}min)",
      c.When.ToString("ddMM HH:mm"), c.FirstName,
      c.LastName, c.Duration);
```

## 输出 2-7

07Aug 08:12 - Barney Gottshall (2min)

07Aug 09:23 - Ariel Hazelgrove (15min)

07Aug 10:5 - Mack Kamph (1min)

08Jul 14:37 - Armando Valdes (13min)

08May 15:23 - Chance Lard (16min)

08Jun 17:12 - Mack Kamph (24min)

为了演示 LINQ to Objects 查询功能的强大之处，列表 2-13 显示的查询通过连接、分组以及在 select 子句中使用聚合操作符，汇总了两个内存集合的数据。该查询的最终输出如输出 2-8。

# 第 2 章 介绍 LINQ TO OBJECTS
