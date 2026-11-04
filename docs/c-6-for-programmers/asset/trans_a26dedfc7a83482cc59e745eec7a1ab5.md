
语句。然而，当执行第 81 行时，Count 和 Capacity 均为 4，因此 List 将其 Capacity 翻倍为 8，Count 变为 5，从而留下可再容纳三个元素的空间。

## 容量翻倍

当 List 增长时，它必须（在后台）创建一个更大的内部数组，并将每个元素复制到新数组中。这是一个耗时的操作。如果每次添加元素时 List 都增长，效率会很低。为了尽量减少内存重新分配的次数，List 在需要更多内存时会将其容量翻倍。¹

> **性能提示 9.1**
> 
> *将 List 的容量翻倍是一种让 List 快速增长到“大致合适的大小”的高效方式。此操作比仅按容纳所添加元素所需的空间来增长 List 要高效得多。缺点是 List 可能占用比所需更多的空间。这是空间/时间权衡的经典示例。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_296_0.png)

> **性能提示 9.2**
> 
> *当需要更多空间时，将 List 的大小翻倍可能会造成浪费。例如，一个包含 1,000,000 个元素的满 List 在添加一个新元素时会调整大小以容纳 2,000,000 个元素。这会留下 999,999 个未使用的元素。你可以使用 TrimExcess（如你的 List 对象中那样）将 List 的容量减少到其当前 Count。你也可以直接设置 Capacity 来更好地控制空间使用——例如，如果你知道某个 List 永远不会超过 100 个元素，可以通过将 100 赋给该 List 的 Capacity，或使用接收初始容量的 List 构造函数来预分配该空间。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_296_1.png)

## 9.5 使用 LINQ 查询泛型 List 集合

与数组一样，你可以使用 LINQ to Objects 查询 List。在图 9.7 中，一个字符串 List 被转换为大写，并搜索以 "R" 开头的项。

```csharp
// Fig. 9.7: LINQWithListCollection.cs
// LINQ to Objects using a List<string>.
using System;
using System.Linq;
using System.Collections.Generic;

class LINQWithListCollection
{
    static void Main()
    {
        // populate a List of strings
        var items = new List<string>();
        items.Add("aQua"); // add "aQua" to the end of the List
        items.Add("RuSt"); // add "RuSt" to the end of the List
        items.Add("yElLoW"); // add "yElLoW" to the end of the List
        items.Add("rEd"); // add "rEd" to the end of the List
18        // display initial List
19        Console.Write("items contains:");
20        foreach (var item in items)
21        {
22            Console.Write($"{item}");
23        }
24
25        Console.WriteLine(); // output end of line
26
27        // convert to uppercase, select those starting with "R" and sort
28        var startsWithR =
29            from item in items
30            let uppercaseString = item.ToUpper()
31            where uppercaseString.StartsWith("R")
32            orderby uppercaseString
33            select uppercaseString;
34
35        // display query results
36        Console.Write("results of query startsWithR:");
37        foreach (var item in startsWithR)
38        {
39            Console.Write($"{item}");
40        }
41
42        Console.WriteLine(); // output end of line
43
44        items.Add("rUBY"); // add "rUBY" to the end of the List
45        items.Add("saffron"); // add "saffron" to the end of the List
46
47        // display initial List
48        Console.Write("items contains:");
49        foreach (var item in items)
50        {
51            Console.Write($"{item}");
52        }
53
54        Console.WriteLine(); // output end of line
55
56        // display updated query results
57        Console.Write("results of query startsWithR:");
58        foreach (var item in startsWithR)
59        {
60            Console.Write($"{item}");
61        }
62
63        Console.WriteLine(); // output end of line
64    }
65 }
```

```text
items contains: aQua RuSt yElLoW rEd
results of query startsWithR: RED RUST
items contains: aQua RuSt yElLoW rEd rUBY saffron
results of query startsWithR: RED RUBY RUST
```

**图 9.7** 使用 List<string> 的 LINQ to Objects。（第 1 部分，共 2 部分。）

**图 9.7** 使用 List<string> 的 LINQ to Objects。（第 2 部分，共 2 部分。）

1. 这不是必需的，并且可能取决于具体实现。

### 9.5.1 let 子句

第 30 行使用 LINQ 的 let 子句创建一个新的范围变量。如果你需要存储临时结果以便在 LINQ 查询后面使用，这会很有用。通常，let 声明一个新的范围变量，并将对查询原始范围变量进行运算的表达式结果赋给该变量。在本例中，我们使用 string 方法 `ToUpper` 将每个项转换为大写，然后将结果存储到新的范围变量 `uppercaseString` 中。然后，我们在 `where`、`orderby` 和 `select` 子句中使用 `uppercaseString`。`where` 子句（第 31 行）使用 string 方法 `StartsWith` 确定 `uppercaseString` 是否以字符 "R" 开头。方法 `StartsWith` 执行区分大小写的比较，以确定字符串是否以作为参数接收的字符串开头。如果 `uppercaseString` 以 "R" 开头，则方法 `StartsWith` 返回 true，该元素会被包含在查询结果中。使用第 16 章《字符串与字符：深入探讨》在线部分（http://www.deitel.com/books/CSharp6FP/）中介绍的正则表达式功能，可以进行更强大的字符串匹配。

### 9.5.2 延迟执行

我们只创建一次查询（第 29–33 行），但遍历结果（第 37–40 行和第 58–61 行）却得到两个不同的颜色列表。这演示了 LINQ 的延迟执行。LINQ 查询仅在你访问结果时执行——例如遍历结果或使用 Count 方法——而不是在定义查询时执行。这使你能够创建一次查询并多次执行它。每次执行查询时，数据源中的任何更改都会反映在结果中。

> **性能提示 9.3**
> 
> *当查询结果不是立即需要时，延迟执行可以提高性能。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_298_0.png)

### 9.5.3 扩展方法 ToArray 和 ToList

有时你可能希望立即检索结果集合。LINQ 为此提供了扩展方法 ToArray 和 ToList。这些方法会执行调用它们的查询，并分别以数组或 List<T> 的形式返回结果。我们在第 19.12 节中使用 ToArray。

> **性能提示 9.4**
> 
> *如果你要多次遍历相同的结果，方法 ToArray 和 ToList 也可以提高效率，因为查询只会执行一次。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_298_1.png)

### 9.5.4 集合初始化器

集合初始化器提供了一种方便的语法（类似于数组初始化器）来初始化集合。例如，图 9.7 的第 12–16 行可以替换为以下语句：

```csharp
var items = new List<string> { "aQua", "RuSt", "yElLoW", "rEd" };
```

在前面的声明中，我们使用 new 显式创建了 List<string>，因此编译器知道初始化器列表包含的是 List<string> 的元素。下面的声明会生成编译错误，因为编译器无法确定你希望创建数组还是集合。

```csharp
var items = { "aQua", "RusT", "yElLoW", "rEd" };
```

## 9.6 小结

本章介绍了 LINQ（Language Integrated Query），这是一个用于查询数据的强大功能。我们展示了如何使用 LINQ 的 where 子句筛选数组或集合，以及如何使用 orderby 子句对查询结果排序。我们使用 select 子句选择对象的特定属性，并使用 let 子句引入新的范围变量，使编写查询更加方便。使用 string 类的 StartsWith 方法筛选以指定字符或字符序列开头的字符串。我们使用了几个 LINQ 扩展方法来执行查询语法未提供的操作——使用 Distinct 方法从结果中移除重复项，使用 Any 方法确定结果是否包含任何项，以及使用 First 方法检索结果中的第一个元素。

我们介绍了 List<T> 泛型集合，它提供了数组的所有功能，以及动态调整大小等其他有用功能。我们使用 Add 方法将新项追加到 List 末尾，使用 Insert 方法将新项插入 List 中的指定位置，使用 Remove 方法移除指定项的第一次出现，使用 RemoveAt 方法移除指定索引处的项，并使用 Contains 方法确定某项是否在 List 中。我们使用 Count 属性获取 List 中的项数，并使用 Capacity 属性确定 List 在不增长的情况下可以容纳的元素数。我们将在后续章节中使用 LINQ 的更高级功能。

在第 10 章中，我们将更深入地研究类概念。我们将讨论 this 引用、其他构造函数概念、运行时如何通过垃圾回收管理内存、静态类成员、只读类成员、对象初始化器和运算符重载。

## 9.7 Deitel LINQ 资源中心

我们的 LINQ 资源中心（http://www.deitel.com/LINQ/）包含许多指向其他信息的链接，包括 Microsoft LINQ 团队成员的博客、书籍、示例章节、常见问题解答、教程、视频、网络广播等。

