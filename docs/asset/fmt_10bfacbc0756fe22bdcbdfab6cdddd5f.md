
```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    IEnumerable<Patent> patents = PatientData.Patents;
    IEnumerable<Patent> patentsOf1800 = patents.Where(
        patent => patent.YearOfPublication.StartsWith("18"));
    IEnumerable<string> items = patentsOf1800.Select(
        patent => patent.ToString());

    Print(items);
}
// ... ...
```

在列表 15.11 中，我们创建了一个新的 `IEnumerable<string>` 集合。在这种情况下，添加 `Select()` 调用并没有改变输出——但仅仅是因为 `Print()` 的 `Console.WriteLine()` 调用本身就使用了 `ToString()`。显然，每个项都从原始集合的 `Patent` 类型转换为了项集合的 `string` 类型。

考虑列表 15.12 中使用 `System.IO.FileInfo` 的示例。

### 列表 15.12：使用 System.Linq.Enumerable.Select() 和 new 进行投影

```csharp
// ...
IEnumerable<string> fileList = Directory.GetFiles(
    rootDirectory, searchPattern);
IEnumerable<FileInfo> files = fileList.Select(
    file => new FileInfo(file));
// ...
```

这里 `file` 的类型是 `IEnumerable<string>`。然而，使用 `Select` 提供的投影，我们可以将集合中的每个项转换为 `System.IO.FileInfo` 对象。

最后，利用元组，我们可以创建一个 `IEnumerable<T>` 集合，其中 `T` 是元组（参见列表 15.13 和输出 15.3）。

### 列表 15.13：投影到元组

```csharp
// ...
IEnumerable<string> fileList = Directory.EnumerateFiles(rootDirectory, searchPattern);
IEnumerable<(string FileName, long Size)> items = fileList.Select(
file => {
    FileInfo fileInfo = new FileInfo(file);
    return (
        FileName: fileInfo.Name,
        Size: fileInfo.Length
    );
});
// ...
```

### 输出 15.3

| FileName = AssemblyInfo.cs, Size = 1704 |

| FileName = CodeAnalysisRules.xml, Size = 735 |

| FileName = CustomDictionary.xml, Size = 199 |

| FileName = EssentialSharp.sln, Size = 4015 |

| FileName = EssentialSharp.suo, Size = 45656 |

| FileName = EssentialSharp.csproj, Size = 98 |

| FileName = EssentialSharp.ConsoleTester.dll, Size = 24576 |

| FileName = intellicher.ConsoleTester.db, Size = 30208 |

匿名类型的输出会自动显示属性名和值，这些是与匿名类型相关的生成的 `ToString()` 方法的一部分。

使用 `Select()` 方法进行投影是非常强大的。我们已经看到了如何使用 `Where()` 标准查询操作符对集合进行垂直方向过滤（减少集合中项的数量）。现在，通过 `Select()` 标准查询操作符，我们还可以从水平方向减少集合（使列数更少）或完全转换数据。`Where()` 和 `Select()` 结合使用提供了一种提取原始集合中当前算法所需的特定部分的方法。仅这两种方法就提供了一个强大的集合操作 API，如果没有这些它们，代码将变得复杂得多，且可读性更差。

# 第15章：带标准查询操作符的集合

## 高级主题

### 并行执行 LINQ 查询

随着具有多个处理器和核心的计算机的普及，利用多核心的能力变得越来越重要。为了实现这一点，程序需要支持多线程。列表 15.14 显示了使用并行 LINQ `PLINQ` 的方法。

### 列表 15.14：并行执行 LINQ 查询

```csharp
// ...
IEnumerable<string> fileList = Directory.EnumerateFiles(rootDirectory, searchPattern);
var items = fileList.AsParallel().Select(file => {
    FileInfo fileInfo = new FileInfo(file);
    return new {
        FileName = fileInfo.Name,
        Size = fileInfo.Length
    };});
```

如列表 15.14 所示，代码即可启用并行。需要注意的一个注意事项（这也是它作为高级主题而不是正文的原因）是并行执行可能会引入竞态条件，导致一个线程上的操作与另一个线程上的操作交织，从而引起数据损坏。为了避免这个问题，对多线程访问的数据需要同步机制，以强制操作的原子性。然而，同步本身可能会引入死锁，进一步增加编程的复杂性。

关于此以及其他多线程主题将在第 19 至 22 章中提供。

## 使用 Count() 计数元素

对集合项经常执行的另一个查询是获取计数。为了支持这种查询，LINQ 包含了 `Count()` 扩展方法。

列表 15.15 展示了 `Count()` 有重载，可以简单计算所有元素（无参数），或者接受一个谓词来计算由该谓词识别的项。

### 列表 15.15：使用 Count() 计数

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
{
        IEnumerable<Patent> patents = PatientData.Patents;
        Console.WriteLine($"专利数量: {patents.Count()}");
        Console.WriteLine($"1800年代的专利数量: {
            patents.Count(patent =>
                patent.YearOfPublication.StartsWith("18"))
        )}");
        // ...
    }
}
```

尽管 `Count()` 语句看起来简单，但 `IEnumerable<T>` 并没有改变，因此执行的代码仍然遍历集合中的所有项。每当集合上直接提供 `Count` 属性时，使用该属性优于 LINQ 的 `Count()` 方法（微妙的区别）。幸运的是，`ICollection<T>` 包含了 `Count` 属性，因此对支持 `ICollection<T>` 的集合调用 `Count()` 方法的代码将直接调用集合的 `Count`。然而，不支持 `ICollection<T>`，

## 第 15 章：带有标准查询操作符的集合接口

`Enumerable.Count()` 将遍历集合中的所有项，而不是调用内置的 Count 机制。如果检查数量的目的是为了查看它是否大于零（`if(patents.Count() > 0){...}`），更优的方法是使用 `Any()` 操作符（`if(patents.Any()){...}`）。`Any()` 尝试遍历集合中的一个项以返回真结果，而不是遍历整个序列。

![](img/b18af4770e9195628243fa73ff1469b4_710_0.png)

## 延迟执行

使用 LINQ 时需要记住的最重要概念之一是延迟执行。考虑列表 15.16 中的代码以及输出 15.4 中的相应输出。

> 列表 15.16：使用 System.Linq.Enumerable.Where() 进行过滤

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

IEnumerable<Patent> patents = PatentData.Patents;
bool result = patents.Where(
    patent =>
    {
        if (result = patent.YearOfPublication.StartsWith("18"))
        {
            // 谓词中的此类副作用
            // 在这里被用于演示一个
            // 原则，通常应该被避免
            Console.WriteLine("\t" + patent);
        }
        return result;
    });
```

## 标准查询操作符

### 输出 15.4

+ 1. 1900 年之前的专利有：

   留声机 (1877)

   活动电影机 (1888)

   电电报 (1837)

   蒸汽机车 (1815)

2. 1900 年之前的专利的第二次列表：

   留声机 (1877)

   活动电影机 (1888)

   电报报 (1837)

   蒸汽机车 (1815)

   1900 年之前有 4 个专利。

3. 1900 年之前的专利的第三次列表：

   留声机 (1877)

   活动电影机 (1888)

   电电报 (1837)

   蒸汽机车 (1815)

   1900 年之前有 4 个专利。

> * 注意 `Console.WriteLine("1. Patents prior...")` 在 lambda 表达式之前执行。识别这一特性非常重要，因为对于那些不知道其重要性的人来说，这并不显而易见。通常，谓词应该只做一件事——评估条件——并且不应该有任何副作用（即使像本例一样打印到控制台）。

## 第 15 章：带有标准查询操作符的集合接口

理解发生了什么，请记住 lambda 表达式是委托——对方法的引用——是可以到处传递的。在 LINQ 和标准查询操作符的上下文中，每个 lambda 表达式都形成了要执行的整体查询的一部分。

在声明时，lambda 表达式并不会执行。事实上，直到 lambda 表达式被调用，其内部的代码才会开始执行。图 15.2 显示了操作顺序。

如图 15.2 所示，列表 15.14 中的三次调用触发了 lambda 表达式，而且每次调用都是相当隐式的。如果 lambda 表达式开销很大（例如调用数据库），那么尽量减少 lambda 表达式的执行将至关重要。

首先，执行是在 `foreach` 循环内部触发的。正如本章前面所述，`foreach` 循环被分解为 `MoveNext()` 调用，每次调用都会导致原始集合中每个项执行 lambda 表达式。在迭代期间，运行时会为每个项调用 lambda 表达式，以确定它是否满足谓词。

其次，对 `Enumerable.Count()`（函数）的调用会再次触发每个项的 lambda 表达式。再次，这是一种微妙的行为，因为 `Count`（属性）在未使用标准查询操作符查询的集合上非常常见。

第三，对 `ToArray()`（或 `ToList()`、`ToDictionary()` 或 `ToLookup()`）的调用会评估每个项的 lambda 表达式。然而，使用这些“To” 方法之一转换集合是非常帮助的。这样做返回的是一个已经执行了标准查询操作符的集合。在列表 15.14 中，转换为数组意味着在最后的 `Console.WriteLine()` 中调用 `Length` 时，`patents` 指向的底层对象实际上是一个数组（实现了 `IEnumerable<T>`）；随后，会调用 `System.Array` 对 `Length` 的实现。因此，在转换为由“To”方法返回的集合类型之一后，通常处理该集合是安全的（直到调用另一个标准查询操作符为止）。但是，请注意，这将整个结果集带入内存（在此步骤之前，它可能由数据库或文件支持）。此外，“To”方法将获取数据的快照，因此在重新查询时会返回新的结果![](img/b18af4770e9195628243fa73ff1469b4_710_0.png)

图 15.2：操作顺序

## 第 15 章：集合接口

为了理解理解发生了什么，请记住 lambda 表达式是委托——对方法的引用——是可以到处传递的。在 LINQ 和标准查询操作符的上下文中，每个 lambda 表达式都形成了要执行的整体查询的一部分。

在声明时，lambda 表达式并不会执行。事实上，直到 lambda 表达式被调用，其内部的代码才会开始执行。图 15.2 显示了操作顺序。

如图 15.2 所示，列表 15.14 中的三次调用触发了 lambda 表达式，而且每次调用都是相当隐式的。如果 lambda 表达式开销很大（例如调用数据库），那么尽量减少 lambda 表达式的执行将至关重要。

首先，执行是在 `foreach` 循环内部触发的。正如本章前面所述，`foreach` 循环被分解为 `MoveNext()` 调用，每次调用都会导致原始集合中每个项执行 lambda 表达式。在迭代期间，运行时会为每个项调用 lambda 表达式，以确定它是否满足谓词。

其次，对 `Enumerable.Count()`（函数）的调用会再次触发每个项的 lambda 表达式。再次，这是一种微妙的行为，因为 `Count`（属性）在未使用标准查询操作符查询的集合上非常常见。

第三，对 `ToArray()`（或 `ToList()`、`ToDictionary()` 或 `ToLookup()`）的调用会评估每个项的 lambda 表达式。然而，使用这些“To”方法转换集合是非常帮助的。这样做返回的是一个已经执行了标准查询操作符的集合。在列表 15.14 中，转换为数组意味着在最后的 `Console.WriteLine()` 中调用 `Length` 时，`patents` 指向的底层对象实际上是一个数组（实现了 `IEnumerable<T>`）；随后，会调用 `System.Array` 对 `Length` 的实现。因此，在转换为由“To”方法返回的集合类型之一后，通常处理该集合是安全的（直到调用另一个标准查询操作符为止）。但是，请注意，这将整个结果集带入内存（在此步骤之前，它可能由数据库或文件支持）。此外，“To”方法将获取数据的快照，因此在重新查询时会返回新的结果![](/b18af4770e9195628243fa73ff1469b4_710_0.png)

图 15.2：操作顺序

## 第 15 章：集合接口

强烈建议你查看 1900 年之前的专利。为了理解...

1. 1900 年之前的专利有：

   留声机 (1877)

   活动电影机 (1888)

   电电报 (1837)

   蒸汽机车 (1815)

2. 1900 年之前的专利的第二次列表：

   留声机 (1877)

   活动电影机 (1888)

   电电报 (1837)

   蒸汽机车 (1815)

   1900 年之前有 4 个专利。

3. 1900 年之前的专利的第三次列表：

   留声机 (1877)

   活动电影机 (1888)

   电电报 (1837)

   蒸汽机车 (1815)

   1900 年之前有 4 个专利。

> * 注意 `Console.WriteLine("1. Patents prior...")` 在 lambda 表达式之前执行。识别这一特性非常重要，因为对于那些不知道其重要性的人来说，这并不显而易见。通常，谓词应该只做一件事——评估条件——并且不应该有任何副作用（即使像本例一样打印到控制台）。

## 使用 OrderBy() 排序

集合的一种常见操作是对其进行排序。排序涉及到对 `System.Linq.OrderBy()` 的调用，如列表 15.16 和输出 15.4 所示。

> 列表 15.16：使用 System.Linq.Enumerable.Where() 进行过滤

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

IEnumerable<Patent> patents = PatentData.Patents;
bool result = patents.Where(
    patent =>
    {
        if (result = patent.YearOfPublication.StartsWith("18"))
        {
            // 谓词中的此类副作用
            // 在这里被用于演示一个
            // 原则，通常应该被避免
            Console.WriteLine("\t" + patent);
        }
        return result;
    });
```

## 标准查询操作符

### 输出 15.4

+ 1. 1900 年之前的专利有：
