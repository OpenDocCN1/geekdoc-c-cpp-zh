
```csharp
System.Collections.ArrayList fruits = new System.Collections.ArrayList(2);
fruits.Add("Mango");
fruits.Add("Orange");
// ApplyOfType<T>()
IEnumerable<string> query = fruits.OfType<string>();
Console.WriteLine("Elements of type 'string':");
foreach (string fruit in query)
    Console.WriteLine(fruit);

// 这段代码的运行结果是：
Elements of type 'string':
Mango
Orange
```

图 4.8 OfType 操作符示例代码。

图 4.8 显示了使用该操作符的代码片段。`OfType<T>(IEnumerable)` 方法仅返回源中可以转换为 T 的元素。如果要在元素无法转换为指定类型时接收异常，请使用 `Cast<T>(IEnumerable)`。

该方法是少数几个可以应用于非参数化类型集合（如 `ArrayList`）的标准查询方法之一。这是因为 `OfType<TResult>` 扩展了 `IEnumerable<T>` 类型，不仅可以应用于基于参数化 `IEnumerable<T>` 类型的集合，还可以应用于实现 `IEnumerable` 的集合。

通过对实现 `IEnumerable` 的集合应用 `OfType<TResult>`，你可以获得使用标准查询操作符查询集合的能力。例如，为 `OfType<TResult>` 指定 Object 类型参数将在 C# 中返回一个 `IEnumerable<Object>` 类型的对象，可以对该对象应用标准查询操作符。

### OrderBy（排序目的）

此操作符方法用于根据 `keySelector` 升序排序输入序列中的元素。输出序列将是 `IOrderedEnumerable<T>` 类型的有序序列。`IEnumerable` 和 `IQuery` 类都包含此操作符。图 4.9 显示了使用该操作符的示例。

```csharp
public static void OrderByEx()
{
    Pet[] pets = new Pet[] { new Pet { Name="Barley", Age=8 },
                             new Pet { Name="Boots", Age=4 },
                             new Pet { Name="Whiskers", Age=1 } };
    IEnumerable<Pet> query = pets.OrderBy(pet => pet.Age);
    foreach (var pet in query)
        Console.WriteLine("{0} - {1}", pet.Name, pet.Age);
}

// 这段代码的运行结果是：
Whiskers - 1
Boots - 4
Barley - 8
```

图 4.9 OrderBy 操作符示例代码。

```csharp
IEnumerable<int> squares = Enumerable.Range(1, 5).Select(x => x * x);
foreach (int num in squares)
    Console.WriteLine(num);
```

// 这段代码的运行结果是：

- 1

- 4

- 9

- 16

- 25

# 图 4.10 Select 选择符的示例代码。

# Select（投影目的）

`IEnumerable` 和 `IQueryable` 类都包含此操作符方法。该方法通过延迟执行实现。立即返回的值是一个存储了执行该操作所需的所有信息的对象。该方法表示的查询在直接调用 `GetEnumerator` 方法或在 Visual C# 中使用 `foreach` 执行对象之前是不会执行的。此投影方法通过转换函数选择器（selector），为源序列中的每个值产生一个值。如果选择器返回的值本身是一个集合，则由调用者手动遍历子序列。在这种情况下，让查询返回一个单一合并的值序列可能更好。要实现这一点，请使用 `SelectMany` 方法代替 `Select`。尽管 `SelectMany` 在返回之前的工作原理与 `Select` 类似。在查询语法中，Visual C# 子句中的 `select` 翻译为调用 `Select`。`where` 子句翻译为调用 `Where`。由于图 4.10 显示了使用该操作符的示例代码。

# Where（限制目的）

`IEnumerable` 和 `IQueryable` 类都包含此操作符方法。该方法通过延迟执行实现。立即返回的值是一个存储了执行该操作所需的所有信息的对象。该方法表示的查询在直接调用 `GetEnumerator` 方法或在 Visual C# 中使用 `foreach` 执行对象之前是不会执行的。图 4.11 显示了使用该操作符的示例代码。在查询语法中，Visual C# 子句中的 `where` 翻译为调用 `Where <TSource,IEnumerable<TSource>,Func<TSource,Boolean>>`。

```csharp
List<string> fruits = new List<string>{"apple", "banana", "mango", "orange", "blueberry", "grape", "strawberry" };
IEnumerable<string> query = fruits.Where(fruit => fruit.Length < 6);
foreach (string fruit in query)
    Console.WriteLine(fruit);

// 这段代码的运行结果是：
apple
mango
grape
```

# 图 4.11 Where 操作符的示例代码。

# 语言集成查询 (LINQ) 简介

```csharp
// 创建字符串数组
string[] names = { "Hartono, Tommy", "Adams, Terry", "Andersen, Henriette", "Hedlund, Magnus", "Ito, Shu" };
string name = names.ElementAt(2);
Console.WriteLine("The name chosen is {0}", name);
// 这段代码的运行结果是：
Andersen, Henriette
```

图 4.12 ElementAt 操作符的示例代码。

# 使用 C# 进行 SQL Server 数据库编程

```c
int[] numbers = { 9, 34, 65, 92, 87, 435, 3, 54, 83, 27, 67, 12, 19 };
int last = numbers.Last();
Console.WriteLine(last);
// 这段代码的运行结果是 19
```

图 4.14 Last运算符的示例代码。

```c
string[] fruits = { "orange" };
string fruit1 = fruits.Single();
Console.WriteLine(fruit1);
// 这段代码的运行结果是 orange
```

图 4.15 Single运算符的示例代码。

**ToArray（转换用途）**

此方法将集合转换为数组。此方法强制执行查询。

`ToArray<TSource>(IEnumerable<TSource>)` 方法强制立即求值并返回包含查询结果的 `List<TSource>`。你可以将此方法附加查询中，以便获取查询结果的缓存副本。

图 4.16 显示了使用该运算符的代码。

**ToList（转换用途）**

此方法将集合转换为 `List`。此方法强制执行查询。

`ToList<TSource>(IEnumerable<TSource>)` 方法强制立即求值并返回包含查询结果的 `List<T>`。你可以将此方法附加查询中，以便获取查询结果的缓存副本。

图 4.17 显示了使用该运算符的代码。

现在我们对标准查询运算符（Standard Query Operator）方法进行详细讨论，它们是执行以完成 LINQ 查询的实际方法。接下来，我们将讨论 LINQ 查询。我们按照以下顺序组织这部分：首先我们将

```csharp
public class ToArrayClass
{
    public static void Main()
    {
        string[] sArray = { "G","H","a","a","H", "over", "Jack" };

        string[] names = sArray.OfType<string>().ToArray();
        foreach (string name in names)
            Console.WriteLine(name);
    }
}
// 这段代码的运行结果是：
GHAoverJack
```

图 4.16 ToArray 运算符的示例代码。

# 语言集成查询 (LINQ)简介

```csharp
string[] fruits = { "apple", "banana", "mango", "orange", "blueberry", "grape", "strawberry" };
List<int> lengths = fruits.Select(fruit => fruit.Length).ToList();
foreach (int length in lengths)
    Console.WriteLine(length);
```

// 这段代码的运行结果是：

- 5

6

6

9

5

10

**图 4.17** ToList 运算符的代码。

提供 LINQ 查询的介绍。然后我们将此讨论分为七部分：

- 1. LINQ 的架构与组件

- 2. LINQ to Objects

- 3. LINQ to DataSet

- 4. LINQ to SQL

- 5. LINQ to Entities

- 6. LINQ to XML

- 7. C# 3.0 对 LINQ 的语言增强

三个组件 LINQ to DataSet、LINQ to SQL 和 LINQ to Entities 属于 LINQ to AD.NET。现在让我们从第一部分开始，LINQ 查询的介绍。

## 4.2 LINQ 查询简介

查询基本上是一个从数据源检索数据的表达式。查询通常用特殊语言表示，如 Microsoft Access、SQL Server、Oracle 或 XML 文档。随着时间的推移，针对不同类型的数据源开发了多种语言，例如用于关系型数据库的 SQL 和用于 XML 的 XQuery。开发者必须为他们支持的每种数据源或格式学习新的查询。LINQ 通过使用一致的模型来处理跨各种数据源和格式的数据，简化了这种局面。在 LINQ 查询中，你处理的是对象。你使用相同的标准编码模式来对 XML 文档、SQL 数据库、AD.NET 集合以及任何可用 LINQ 程序的格式进行查询和转换。

LINQ 可以被视为一种由一组标准查询方法支持的模式或模型，所有这些标准查询方法都是定义在 `System.Linq` 命名空间 `IEnumerable` 或 `IQueryable` 类中的静态方法。LINQ 查询中操作的数据是类型为 `IEnumerable<T>` 或 `IQueryable<T>` 的序列对象，其中 T 是存储在序列中的数据的实际类型。

从另一个角度来看，LINQ 也可以作为一个转换器或桥梁，在标准查询运算符中实现的抽象对象与真实世界中实现的物理现实之间建立映射关系。正是 LINQ 允许开发者使用相同的基本编码模式直接访问和操作不同数据库中的数据。在 LINQ 的帮助下，学习和使用不同数据源的不同语法、格式和查询结构以访问和查询它们而带来的困难可以被消除

# 使用 C# 进行 SQL Server 数据库编程

数据库查询的效率可以显著提高，查询过程也可以大大简化。

从结构上，LINQ 查询操作由三个不同的动作组成：

- 1) 获取数据源。

- 2) 创建查询。

- 3) 执行查询。

为了更好地理解 LINQ 及其运行过程。

让我们用示例来说明查询操作的三个部分如何在源代码中表示。为了方便起见，示例使用整数数组作为数据源；但相同的概念也适用于其他数据源。

示例案例如图 4.18 所示。

这段代码的准确运行情况如图所示所示。

关键点在于：在 LINQ 中，查询的执行来自于查询本身；换句话说，当你在第 2 步创建查询时，你还没有检索任何数据，真实的数据查询发生在第 3 步，即使用 `foreach` 循环进行查询执行。

让我们看看这段代码以及映射的过程，以便对 LINQ 查询及其过程有一个清晰的认识。

此示例中使用的**数据源**是一个整数数组 `numbers`，它隐式支持泛型 `IEnumerable<T>` 接口。这一事实意味着查询使用 LINQ 执行，在 fetch 语句中执行，并且需要 `IEnumerable` 或 `IEnumerable<T>` 类型。支持 `IEnumerable<>` 或派生接口（如 `IQueryable<T>`）的类型被称为可查询类型。

**查询**指定了从数据源或数据源中检索哪些信息。可选情况下，查询还指定了信息在返回之前如何进行排序、分组和塑造。查询存储在查询变量中，并用查询表达式初始化。为了更容易编写查询，C# 引入了新的查询语法。

查询表达式的基本形式如图 4.20 所示。

三个子句：**from**、**where** 和 **select** 用于大多数 LINQ 查询。

```csharp
static void IntroLINQ()
{
    // LINQ 查询的三个部分：
    // 1. 数据源。
    int[] numbers = new int[] { 0, 1, 2, 3, 4, 5, 6 };

    // 2. 查询创建。查询是一个 IEnumerable<int>
    var numQuery = from num in numbers
                   where (num % 2) == 0
                   select num;

    // 3. 查询执行。
    foreach (int num in numQuery)
    {
        Console.Write("{0,1}", num);
    }
    // 这段代码的运行结果是：
    0, 2, 4, 6
}
```

**图 4.18** LINQ 查询的代码。

# 语言集成查询 (LINQ)

# 数据源

![](img/d59a47501d0a20fc0460a9c46c6fb7_145_0)

# 查询

# 查询执行

**图 4.19** LINQ 查询的运行过程。

```
from [identifier] in [data source]
let [expression]
where [boolean expression]
order by [expression]([ascending/descending]),optionally repeat
select [expression]
group [expression] into [expression]
```

**图 4.20** 典型的 LINQ 查询表达式。

此示例中的查询返回整数数组中的所有偶数。查询表达式包含三个子句：**from**、**where** 和 **select**。如果你熟悉 SQL，你会发现 SQL 中子句的顺序是反的。**from** 子句指定数据源，**where** 子句应用过滤，**select** 子句指定返回元素的类型。它不返回任何数据。现在的重点是，在 LINQ 中，查询变量本身不采取行动也不返回数据。它存储了在以后执行查询时产生结果所需的信息。

此示例中的**查询执行**是延迟执行，因为此查询中的所有运算符都是延迟运算符（参见图 4.4）。

`foreach` 语句配合迭代变量 `num` 用于从数据源获取每个项并赋值给变量 `num`。执行 `Console.WriteLine()` 方法来显示收到的每个数据项，此查询过程将持续直到从数据源检索所有数据项。

由于查询变量本身从不持有查询结果，你可以随时执行它。例如，你可能有一个被另一个应用程序持续更新的数据库。在你的应用程序中，你可以创建一个获取最新数据的查询，并可以按照某些间隔重复执行，以便每次都获取不同的结果。

对元素源执行聚合函数的查询会首先遍历这些元素。查询示例包括 Count（计数）、Max（最大值）、Average（平均值）和 First（第一个）。这些查询在没有显式 `foreach` 语句的情况下执行，因为查询本身必须使用 `foreach` 来返回结果。注意，此类查询返回的是单个值，而不是 Enumerable（可枚举）集合。要强制执行任何查询并缓存其结果，你可以调用 `ToList<TSource>` 或 `ToArray<TSource>` 方法。你也可以通过在查询表达式后紧跟一个循环来强制执行。通过调用 `ToList` 或 `ToArray`，你还将将所有数据缓存到单个集合对象中。

## 4.3 LINQ 架构与 LINQ 组件

LINQ 由三个主要组件组成：LINQ to Objects（对象 LINQ）、LINQ to ADO.NET 和 LINQ to XML。LINQ 的详细组织结构可以写为：

- 1. LINQ to Objects

- 2. LINQ to ADO.NET (LINQ to DataSet, LINQ to SQL 和 LINQ to Entities)

- 3. LINQ to XML
