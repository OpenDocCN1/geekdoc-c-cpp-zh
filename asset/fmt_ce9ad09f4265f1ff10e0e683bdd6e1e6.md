
# 524 C# 3.0: 初学者指南

```csharp
// 使用 let 子句和嵌套的 from 子句。
using System;
using System.Linq;
class LetDemo {
    static void Main() {
        string[] strs = { "alpha", "beta", "gamma" };
        // 创建一个查询，获取字符串中的字符，
        // 并按排序返回。注意嵌套子句的使用。
        var chrs = from str in strs
            let chrArray = str.ToArray()
            from ch in chrArray
            orderby ch
            select ch;
        Console.WriteLine("按顺序排序的单个字符:");
        foreach (char c in chrs) Console.Write(c + " ");
        Console.WriteLine();
    }
}
```

`chrArray` 指向从 `str` 获取的字符数组。

输出所示：

按顺序排序的单个字符：
a a a a b e g h l m p t

在程序中，`let` 子句如何将 `chrArray` 赋值为 `str.ToArray()` 返回的数组的引用：

```csharp
chrArray = str.ToArray();
```

在 `let` 子句之后，其他可以使用 `chrArray`。此外，由于 C# 中的所有数组都实现了 `IEnumerable<T>`，因此 `chrArray` 可以用作第二个嵌套 `from` 子句的数据源。这正是示例中发生的情况。嵌套的 `from` 枚举数组中的单个字符，将它们按升序排列并返回结果。

你也可以使用 `let` 子句来保存一个非枚举值。例如，这是编写前一节中 `IntDemo` 程序所示查询的更高效的方法。

```csharp
var webAddrs = from addr in websites
    let idx = addr.LastIndexOf(".")
    where idx != -1
```

只调用一次 `LastIndexOf()`，并将结果存储在 `idx` 中。

# 第 14 章：介绍 LINQ 525

```csharp
group addr by addr.Substring(idx)
into ws
where ws.Count() > 2
select ws;
```

在这个版本中，句号最后一次出现的索引被赋值给 `idx`。该值随后被 `Substring()` 使用。这避免了需要两次搜索句号的操作。

## 使用 join 合并两个序列

在处理数据库工作时，创建一个关联来自两个不同源数据的序列是常见的。例如，一个在线商店可能有一个数据库将项目名称与其项目编号关联，有另一个数据库将项目编号与在库状态关联。给定这种情况，你可能想生成一个列表，按名称显示项目的在库状态，而不是按项目编号。你可以通过关联两个数据库中的数据来实现这一点。在 LINQ 中，通过 `join` 子句很容易实现这种操作。

`join` 的通用形式所示（结合 `from` 子句的上下文）：

```csharp
from rangeVarA in data-sourceA
join rangeVarB in data-sourceB
on rangeVarA.property equals rangeVarB.property
```

使用 `join` 的关键在于理解每个数据源必须包含共同数据，并且这些数据可以进行等值比较。因此，在通用形式中，`data-sourceA` 和 `dataSourceB` 具有可以比较的共同点。正在比较的项目由 `on` 部分指定。因此，当 `rangeVarA.property` 等于 `rangeVarB.property` 时，关联成功。从本质上说，`join` 像过滤器，只允许共享共同值的元素通过。

使用 `join` 时，返回的序列通常是两个不同源的复合。因此，`join` 允许你生成一个包含两个不同源元素的新列表。这使你能够以新的方式组织数据。

以下程序创建了一个 `Item` 类，它封装了项目的名称及其编号。它创建了另一个名为 `InStatus` 的类，它将项目编号与一个指示项目是否在库的布尔属性关联。它还创建了一个名为 `Temp` 的类，它有两个字段：`string` 和 `bool`。该类的对象将持有查询结果。查询使用 `join` 生成一个列表，其中项目的名称与其在库状态相关联。

```csharp
// 演示 join。
using System;
using System.Linq;
```

```csharp
// 将项目名称与其编号关联的类。
class Item {
```

# 526 C# 3.0: 初学者指南

```csharp
public string Name { get; set; }
public int ItemNumber { get; set; }
public Item(string n, int inum) {
    Name = n;
    ItemNumber = inum;
}
```

```csharp
// 将项目编号与其状态关联的类。
class InStatus {
    public int ItemNumber { get; set; }
    public bool InStock { get; set; }
}
public InStatus(int n, bool b) {
    ItemNumber = n;
    InStock = b;
}
```

```csharp
// 封装名称及其状态的类。
class Temp {
    public string Name { get; set; }
    public bool InStock { get; set; }
}
public Temp(string n, bool b) {
    Name = n;
    InStock = b;
}
```

## 第 14 章：引入 LINQ

请记住，当创建一个匿名类型时，你指定的标识符将成为只读的公共属性。因此，它们可以被代码的其他部分使用。

虽然使用了匿名类型，但这并不完全准确！该类型相对于你（即程序员）来说是匿名的。然而，编译器确实给它分配了一个内部名称。因此，匿名类型并没有违反 C# 的强类型检查规则。

为了完全理解匿名类型的价值，请考虑对之前演示 Join（连接）的程序进行重写。回想之前的之前的版本，需要一个名为 `Temp` 的类来封装连接的结果。通过使用匿名类型，这个“占位符”类不再被需要了，也不会让程序的源代码变得杂乱。程序的输出与之前保持一致。

```csharp
// 使用匿名类型改进连接 演示程序。
using System;
using System.Linq;
// 将项目名称与其数字关联的类。
class Item {
    public string Name { get; set; }
    public int ItemNumber { get; set; }
    public Item(string n, int inum) {
        Name = n;
        ItemNumber = inum;
    }
}
// 将项目编号与其库存状态关联的类。
class InStockStatus {
    public int ItemNumber { get; set; }
    public bool InStock { get; set; }
    public InStockStatus(int n, bool b) {
        ItemNumber = n;
        InStock = b;
    }
}
class AnonTypeDemo {
    static void Main() {
        Item[] items = {
            new Item("Pliers", 1424),
            new Item("Hammer", 7892),
            new Item("Wrench", 8534),
            new Item("Saw", 6411)
        };
    }
}
```

# C# 3.0：初学者指南

```csharp
InStockStatus[] statusList = {
    new InStockStatus(1424, true),
    new InStockStatus(7892, false),
    new InStockStatus(8534, true),
    new InStockStatus(6411, true)
};
```

```csharp
// 创建一个连接 Item 和 InStatus 的查询，
// 以产生一个项目类型的列表。
// 现在，来自 item in items 的匿名类型。
var inStockList = join entry in statusList
    on item.ItemNumber equals entry.ItemNumber
    select new { Name = item.Name,
    InStock = entry.InStock };
```

```csharp
Console.WriteLine("Item\tAvailable\n");
```

```csharp
// 执行查询并显示结果。
foreach(var t in inStockList)
    Console.WriteLine("{0}\t{1}", t.Name, t.InStock);
```

注意 `select` 子句：

```csharp
select new { Name = item.Name,
    InStock = entry.InStock };
```
