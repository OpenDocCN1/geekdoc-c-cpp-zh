
```csharp
// 图 21.8: FunctionalProgramming.cs
// 使用 LINQ 扩展方法和 lambda 进行函数式编程。
using System;
using System.Collections.Generic;
using System.Linq;

namespace FilterMapReduce
{
    class FunctionalProgramming
    {
        static void Main()
        {
            var values = new List<int>{3, 10, 6, 1, 4, 8, 2, 5, 9, 7};
            Console.WriteLine("Original values: ");
            values.Display(); // 调用扩展方法

            // 显示 Min, Max, Sum 和 Average
            Console.WriteLine($"\nMin: {values.Min()}");
            Console.WriteLine($"\nMax: {values.Max()}");
            Console.WriteLine($"\nSum: {values.Sum()}");
            Console.WriteLine($"\nAverage: {values.Average()}");

            // 通过 Aggregate 计算求和
            Console.WriteLine("\nSum via Aggregate method: " +
                values.Aggregate(0, (x, y) => x + y));

            // 通过 Aggregate 计算平方和
            Console.WriteLine("\nSum of squares via Aggregate method: " +
                values.Aggregate(0, (x, y) => x + y * y));

            // 通过 Aggregate 计算乘积
            Console.WriteLine("\nProduct via Aggregate method: " +
                values.Aggregate(1, (x, y) => x * y));

            // 按排序顺序显示偶数：
            Console.Write("\neven values displayed in sorted order: ");
            values.Where(value => value % 2 == 0) // 找到偶数
                .OrderBy(value => value) // 对剩余值排序
                .Display(); // 显示结果

}
    }
}
```

**图 21.8** 使用 LINQ 扩展方法和 lambda 进行函数式编程。（2 部分中的第 I 部分。）

```csharp
// 将奇数乘以 10 并按排序顺序显示
Console.Write(
    "Odd values multiplied by 10 displayed in sorted order: "
);
values.Where(value => value % 2 != 0) // 找到奇数
    .Select(value => value * 10) // 每个乘以 10
    .OrderBy(value => value) // 对值排序
    .Display(); // 显示结果

// 再次显示原始值以证明它们没有被修改
Console.Write("\nOriginal values: ");
values.Display(); // 调用 Display 扩展方法

// 声明一个扩展方法
static class Extensions
{
    // 用空格分隔显示所有元素的扩展方法
    public static void Display<T>(this IEnumerable<T> data)
    {
        Console.WriteLine(string.Join(" ", data));
    }
}
```

Original values: 3 10 6 1 4 8 2 5 9 7

Min: 1

Max: 10

Sum: 55

Average: 5.5

Sum via Aggregate method: 55

Sum of squares via Aggregate method: 385

Product via Aggregate method: 3628800

Even values displayed in sorted order: 2 4 6 8 10

Odd values multiplied by 10 displayed in sorted order: 10 30 50 70 90

Original values: 3 10 6 1 4 8 2 5 9 7

> 图 21.8 使用 LINQ 扩展方法和 lambda 进行函数式编程。（2 部分中的第 II 部分。）

## 扩展方法

在整个示例中，我们通过调用扩展方法来显示各种操作的结果，该扩展方法定义在静态类 `Extensions` 中。在 `Main` 的开始和结束，我们对 `IEnumerable<T>` 参数调用 `Display` 以按顺序显示元素。

## 21.11.1 LINQ 扩展方法：Min, Max, Sum 和 Average

类 `Enumerable` 定义了用于执行常见操作的各种 LINQ 扩展方法：

- `Min`（第19行）返回集合中的最小值。
- `Max`（第20行）返回集合中的最大值。
- `Sum`（第21行）返回所有值的总和。
- `Average`（第22行）返回所有值的平均值。

### 迭代和变异对你是隐藏的

事实上，LINQ 操作没有修改原始集合或应用程序中任何变量的副作用——

- 我们只需说想要实现什么，而不是*如何*实现。
- `values` 集合*没有被修改*（由第52行证实）。

当然，在后台需要迭代和可变变量：

- 所有四个扩展方法都会遍历集合并跟踪当前元素。
- 在遍历集合时，`Min` 和 `Average` 分别存储当前的极值，而 `Sum` 和 `Average` 必须跟踪已处理元素的总和——这些操作都会修改局部变量。

21.11.2 到21.11.4节中的其他操作也需要迭代和可变变量，但*库*（已经过调试和测试）为你处理了这些细节。要查看 `Min`、`Max`、`Sum` 和 `Average` 等 LINQ 扩展方法如何实现这些概念，请查看 .NET 源码中的 `Enumerable`：

```
https://github.com/dotnet/corefx/tree/master/src/System.Linq/src/System/Linq
```

## 21.11.2 用于归约操作的 Aggregate 扩展方法

你可以使用 *Aggregate* LINQ 方法定义归约。例如，第25–26行的 `Aggregate` 调用对 `values` 的元素求和。这里使用的 `Aggregate` 版本接收两个参数：

- 第一个参数（0）是帮助你开始归约操作的值。在对集合求和时，从 0 开始。很快我们将使用 1 开始计算元素的乘积。
- 第二个参数是类型为 *Func*（命名空间）的委托，表示一个接收两个相同类型参数并返回一个值的方法——有许多 *Func* 版本可以指定从 0 到 16 个任意类型的参数。

## 21.11 使用 LINQ 方法调用语法和 Lambda表达式进行函数式编程

在这种情况下，我们传递了以下 lambda 表达式，它返回其参数的和：

```
(x, y) => x + y
```

对于集合中的每个元素，`Aggregate` 都会调用此 lambda 表达式。

- 在第一次调用 lambda 时，参数 `x` 的值是 `Aggregate` 的第一个参数 (0)，参数 `y` 的值是 `values` 中的第一个 `int` (3)，产生值 3 (0 + 3)。
- 随后的每次对 lambda 的调用都会使用上一次调的结果作为第一个参数，并将集合中的下一个元素作为第二个参数。在第二次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (3)，参数 `y` 的值是 `values` 中的第二个 `int` (10)，产生总和 13 (3 + 10)。
- 在第三次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (13)，参数 `y` 的值是 `values` 中的第三个 `int` (6)，产生总和 19 (13 + 6)。

此过程会持续运行，直到所有值都使用完毕，此时 `Aggregate` 返回最终总和。注意，没有使用可变变量将集合归约为元素之和，且原始的 `values` 集合没有被修改。

### 使用 Aggregate 方法计算值的平方和

第 29–30 行使用 `Aggregate` 计算 `values` 元素的平方和。在这种情况下，lambda 为：

```
(x, y) => x * y
```

它将当前值的平方加到总和中。归约的评估过程如下：

- 在第一次调用 lambda 时，参数 `x` 的值是 `Aggregate` 的第一个参数 (0)，参数 `y` 的值是 `values` 中的第一个 `int` (3)，产生值 9 (0 + 3²)。
- 在下一次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (9)，参数 `y` 的值是 `values` 中的第二个 `int` (10)，产生总和 109 (9 + 10²)。
- 在下一次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (109)，参数 `y` 的值是 `values` 中的第三个 `int` (6)，产生总和 145 (109 + 6²)。

此过程会持续运行，直到所有元素的平方都使用完毕，此时 `Aggregate` 返回最终总和。再次注意，没有使用可变变量将集合归约为元素的平方和，且原始的 `values` 集合没有被修改。

### 使用 Aggregate 方法计算值的乘积

第 33–34 行使用 `Aggregate` 计算 `values` 元素的乘积。lambda

```
(x, y) => x * y
```

将它的两个参数相乘。因为我们要产生一个乘积，在这种情况下我们从值 1 开始。归约的评估过程如下：

- 在第一次调用 lambda 时，参数 `x` 的值是 `Aggregate` 的第一个参数 (1)，参数 `y` 的值是 `values` 中的第一个 `int` (3)，产生值 3 (1 * 3)。
- 在下一次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (3)，参数 `y` 的值是 `values` 中的第二个 `int` (10)，产生总和 30 (3 * 10)。
- 在下一次调用 lambda 时，参数 `x` 的值是上一次计算的结果 (30)，参数 `y` 的值是 `values` 中的第三个 `int` (6)，产生总和 180 (30 * 6)。

此过程持续持续产生元素的运行乘积，直到所有元素都使用完毕，最后返回最终乘积。注意，没有使用可变变量将集合归约为元素的乘积，且原始的 `values` 集合没有被修改。

### 21.11.3 用于过滤操作的扩展方法

第 38–40 行过滤 `values` 中的整数，按升序排序并显示结果。你通过过滤产生一个匹配特定条件的新结果集合，该条件被称为谓词（predicate）。LINQ 扩展方法 `Where`（第 38 行）接受其参数作为一个 `Func` 委托，该方法接收一个参数并返回一个 `bool`，指示给定元素是否应该包含在返回的集合中。第 38 行的 lambda：

```
value => value % 2 == 0
```

它接收一个值并返回一个 `bool`，指示该值是否满足谓词——在这种情况下，即该值能被 2 整除。

#### 排序结果

`OrderBy` 方法接收其参数作为一个 `Func` 委托，代表该方法接收一个参数并返回一个用于排序结果的值。在这种情况下 (39)，lambda 表达式

```
value => value
```

简单地返回其参数，`OrderBy` 使用它来按升序对值进行排序——如果要按降序排序，可以使用 `OrderDescending`。注意，没有使用可变变量来过滤或排序集合，且原始的 `values` 集合没有被修改。

#### 延迟执行

对 `Where` 和 `OrderBy` 的调用使用了我们在 9.5.2 节讨论过的相同延迟执行——在遍历它们之前，它们不会被评估。在第 38–40 行，这发生在调用我们的 `Display` 扩展方法时（第 40 行）。这意味着你可以将操作保存到变量中执行，如下：

```csharp
var Integers =
    values.Where(value => value % 2 == 0) // 寻找整数
    .OrderBy(value => value); // 排序
```

你可以通过遍历 `Integers` 来执行该操作。

### 21.11.4 用于映射操作的 Select 扩展方法

第 45–48 行过滤 `values` 中的整数，将每个整数乘以 10，按升序排序并显示结果。这种新功能是映射操作，它将集合转换为新值，其类型有时与原始元素不同。LINQ 扩展方法 `Select` 接受其参数作为一个 `Func` 委托，该方法接收一个参数并将其映射为一个值（可能是另一种类型），包含在返回的集合中。第 46 行的 lambda：

```
value => value * 10
```

它将它的值乘以 10。第 47 行排序结果。`Select` 的调用被延迟到遍历结果时——在这种情况下是调用 `Display` 扩展方法时（第 48 行）。注意，没有使用可变变量来映射集合，且原始的 `values` 集合没有被修改。

## 21.12 PLINQ：通过多核提升 LINQ Objects 性能

如今的客户可能拥有具有四个或八核心的处理器。一个供应商提供了 61 核处理器，未来的处理器可能会有更多核心。你的计算机操作系统在操作系统任务和运行的应用程序之间共享核心。

### 线程

线程概念允许系统运行并发线程的一部分——例如，用户界面线程（通常称为 GUI 线程）等待用户与 GUI 控件交互，同一个应用程序中的分离线程可以形成任务，如复杂计算、下载视频、播放音乐、发送电子邮件等。尽管所有这些任务都可以并发进展，但它们可能通过共享一个处理器核心来实现。

### 共享处理器

有了多核处理器，应用程序可以在不同的核心上真正并行（即同时）运行。此外，操作系统允许一个应用程序的线程在不同的核心上并行运行，从而可能大幅提高应用程序的性能。并行化应用程序和算法以利用多个核心是困难且极易出错的，当这些线程共享可以被一个或多个任务修改的数据时。

### PLINQ (并行 LINQ)

在 21.10 节中，我们提到函数式编程和内部迭代的一个优点是，库代码（在后台）会遍历集合的所有元素，一个

- 3. 网站 `http://processors.specout.com` 显示了从 1 到 61 核的处理器范围。

## 第 21 章 通用集合：使用 LINQ/PLINQ 进行函数式编程

执行任务的集合。另一个好处是，你可以轻松地请求库使用并行处理执行任务，以利用处理器的多核心。`PLINQ`（并行 LINQ）的目的是 LINQ to Objects 扩展方法的实现，它通过并行化操作来增强性能。`PLINQ` 为你处理了容易出错的环节：将任务拆分为并行执行的小片段，并协调这些片段的结果，这让你能够更容易地编写出利用多核处理器的高性能应用程序。

### 演示 PLINQ

图 21.9 展示了 LINQ to Objects 和 PLINQ 扩展方法 `Min`、`Max` 和 `Average` 如何于一个包含 10,000,000 个 `int` 值的数组（创建于 13-15 行）。与 LINQ to Objects 一样，PLINQ 版本的这些操作不会修改原始集合。我们对操作进行了计时，以显示 PLINQ（使用多核）相比于 LINQ to Objects（使用单核）的巨大性能提升。在本文的后续讨论中，我们将 LINQ to Objects 简称为 LINQ。
