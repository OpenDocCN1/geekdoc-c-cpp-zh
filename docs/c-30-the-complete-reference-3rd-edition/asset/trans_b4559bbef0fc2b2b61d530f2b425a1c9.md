
值）。可以在 nums 上调用 Where() 方法，因为所有数组都实现了 `IEnumerable<T>`，而该接口支持查询扩展方法。

从技术上讲，前面示例中的 Select() 方法并不是必需的，因为在这种简单情况下，Where() 返回的序列已经包含了结果。不过，你可以像使用查询语法时那样，使用更复杂的选择条件。例如，以下查询返回 nums 中的正值，并将它们放大一个数量级：

```csharp
var posNums = nums.Where(n => n > 0).Select(r => r * 10);
```

正如你可能预料的，你可以将其他操作链接在一起。例如，以下查询选择正值，按降序排序，并返回结果序列：

```csharp
var posNums = nums.Where(n => n > 0).OrderByDescending(j => j);
```

这里，表达式 j => j 指定排序依赖于输入参数，该参数是来自 Where() 所得序列的一个元素。

下面是一个演示 GroupBy() 方法的示例。它改写了前面展示的分组示例。

```csharp
// Demonstrate the GroupBy() query method.
// This program reworks the earlier version that used
// the query syntax.
using System;
using System.Linq;

class GroupByDemo {
    static void Main() {
        string[] websites = { "hsNameA.com", "hsNameB.net", "hsNameC.net",
            "hsNameD.com", "hsNameE.org", "hsNameF.org",
            "hsNameG.tv", "hsNameH.net", "hsNameI.tv" };

        // Use query methods to group websites by top-level domain name.
        var webAddrs = websites.Where(w => w.LastIndexOf(".") != -1).
            GroupBy(x => x.Substring(x.LastIndexOf(".") + 1));

        // Execute the query and display the results.
        foreach(var sites in webAddrs) {
            Console.WriteLine("Web sites grouped by " + sites.Key);
            foreach(var site in sites)
                Console.WriteLine("  " + site);
            Console.WriteLine();
        }
    }
}
```

此版本产生与之前版本相同的输出。唯一的区别在于查询的创建方式。此版本使用的是查询方法。

下面是另一个示例。回想一下前面 JoinDemo 示例中使用的联接查询：

```csharp
var inStockList = from item in items
    join entry in statusList
        on item.ItemNumber equals entry.ItemNumber
    select new Temp(item.Name, entry.InStock);
```

该查询生成一个序列，其中包含封装了库存项目名称和现货状态的对象。这些信息是通过联接 items 和 statusList 两个列表合成的。以下版本改写了这个查询，使其使用 Join() 方法而不是 C# 查询语法：

```csharp
// Use Join() to produce a list of item names and status.
var inStockList = items.Join(statusList,
    k1 => k1.ItemNumber,
    k2 => k2.ItemNumber,
    (k1, k2) => new Temp(k1.Name, k2.InStock) );
```

尽管此版本使用名为 Temp 的命名类来保存结果对象，但也可以改用匿名类型。这种方法如下所示：

```csharp
var inStockList = items.Join(statusList,
    k1 => k1.ItemNumber,
    k2 => k2.ItemNumber,
    (k1, k2) => new { k1.Name, k2.InStock} );
```

## 查询语法与查询方法

如前一节所述，C# 有两种创建查询的方式：查询语法和查询方法。有趣的是，仅通过查看程序的源代码并不容易看出，这两种方法之间的关系比你最初设想的要紧密得多。原因是查询语法会被编译为对查询方法的调用。因此，当你编写类似如下的代码时：

```csharp
where x < 10
```

编译器会将其转换为

```csharp
Where(x => x < 10)
```

因此，创建查询的两种方法最终殊途同归。鉴于这两种方法最终是等价的，自然会产生以下问题：哪种方法最适合 C# 程序？答案是：一般而言，你会希望使用查询语法。它完全集成在 C# 语言中，得到关键字和语法的支持，并且更加简洁。

## 更多与查询相关的扩展方法

除了与 C# 支持的查询关键字对应的方法之外，.NET Framework 还提供了其他一些在查询中经常有用的查询相关扩展方法。这些与查询相关的方法由 Enumerable 为 `IEnumerable<T>` 定义。以下是一些常用方法的示例。由于许多方法都有重载，这里仅显示其一般形式。

| 方法 | 描述 |
|---|---|
| All(condition) | 如果序列中的所有元素都满足指定条件，则返回 true。 |
| Any(condition) | 如果序列中的任一元素满足指定条件，则返回 true。 |
| Average() | 返回数值序列中值的平均值。 |
| Contains(obj) | 如果序列包含指定对象，则返回 true。 |
| Count() | 返回序列的长度，即序列中包含的元素个数。 |
| First() | 返回序列中的第一个元素。 |
| Last() | 返回序列中的最后一个元素。 |
| Max() | 返回序列中的最大值。 |
| Min() | 返回序列中的最小值。 |
| Sum() | 返回数值序列中值的总和。 |

在本章前面你已经看到 Count() 的实际用法。下面这个程序演示了其他方法：

```csharp
// Use several of the extension methods defined by Enumerable.
using System;
using System.Linq;

class ExtMethods {
    static void Main() {

        int[] nums = { 3, 1, 2, 5, 4 };

        Console.WriteLine("The minimum value is " + nums.Min());
        Console.WriteLine("The maximum value is " + nums.Max());

        Console.WriteLine("The first value is " + nums.First());
        Console.WriteLine("The last value is " + nums.Last());

        Console.WriteLine("The sum is " + nums.Sum());
        Console.WriteLine("The average is " + nums.Average());

        if(nums.All(n => n > 0))
            Console.WriteLine("All values are greater than zero.");

        if(nums.Any(n => (n % 2) == 0))
            Console.WriteLine("At least one value is even.");

        if(nums.Contains(3))
            Console.WriteLine("The array contains 3.");
    }
}
```

输出如下所示：

```text
The minimum value is 1
The maximum value is 5
The first value is 3
The last value is 4
The sum is 15
The average is 3
All values are greater than zero.
At least one value is even.
The array contains 3.
```

你还可以在基于 C# 查询语法的查询中使用与查询相关的扩展方法。事实上，这是很常见的做法。例如，以下程序使用 Average() 获取一个序列，该序列仅包含数组中小于平均值的那些值。

```csharp
// Use Average() with the query syntax.
using System;
using System.Linq;

class ExtMethods2 {
    static void Main() {
        int[] nums = { 1, 2, 4, 8, 6, 9, 10, 3, 6, 7 };
        var ltAvg = from n in nums
                    let x = nums.Average()
                    where n < x
                    select n;
        Console.WriteLine("The average is " + nums.Average());
        Console.Write("These values are less than the average: ");
        // Execute the query and display the results.
        foreach(int i in ltAvg) Console.Write(i + " ");
        Console.WriteLine();
    }
}
```

输出如下所示：

```text
The average is 5.6
These values are less than the average: 1 2 4 3
```

请特别注意以下查询：

```csharp
var ltAvg = from n in nums
            let x = nums.Average()
            where n < x
            select n;
```

注意在 let 语句中，x 被设置为 nums 中值的平均值。该值是通过在 nums 上调用 Average() 获得的。

## 查询的延迟执行与立即执行

在 LINQ 中，查询有两种不同的执行模式：立即执行和延迟执行。正如本章前面所解释的，查询定义了一组规则，这些规则实际上不会执行，直到执行 foreach 语句。这被称为延迟执行。

但是，如果使用某个产生非序列结果的扩展方法，那么必须执行查询才能获得该结果。例如，考虑 Count() 方法。为了让 Count() 返回序列中的元素个数，必须执行查询，而这在调用 Count() 时会自动完成。在这种情况下，会进行立即执行，查询自动执行以获得结果。因此，即使你没有在 foreach 循环中显式使用查询，查询仍会被执行。

下面是一个简单示例。它获取序列中正元素的数量。

```csharp
// Use immediate execution.
using System;
using System.Linq;

class ImmediateExec {
  static void Main() {
    int[] nums = { 1, -2, 3, 0, -4, 5 };

    // Create a query that obtains the number of positive
    // values in nums.
    int len = (from n in nums
               where n > 0
               select n).Count();

    Console.WriteLine("The number of positive values in nums: " + len);
  }
}
```

输出为

```text
The number of positive values in nums: 3
```

在程序中，注意没有指定显式的 foreach 循环。相反，由于调用了 Count()，查询会自动执行。

有趣的是，前面程序中的查询也可以这样写：

```csharp
var posNums = from n in nums
              where n > 0
              select n;

int len = posNums.Count(); // query executes here
```

在这种情况下，对查询变量调用 Count()。此时，查询被执行以获得数量。

另外两个导致查询立即执行的方法分别是 ToArray() 和 ToList()。两者都是 Enumerable 定义的扩展方法。ToArray() 返回结果
