
集合以执行任务。另一个好处是，您可以轻松地要求库使用 *并行处理* 执行任务，以利用处理器的多个核心。这是 PLINQ（Parallel LINQ）的目的——LINQ to Objects 扩展方法的实现，可并行化操作以提高性能。PLINQ 为您处理将任务分解为可 *并行* 执行的较小部分以及协调这些部分结果的容易出错的方面，使您更容易编写利用多核处理器的高性能应用程序。

## *演示 PLINQ*

图 19.9 演示了 LINQ to Objects 和 PLINQ 扩展方法 Min、Max 和 Average 在一个包含 10,000,000 个随机 int 值（在第 13–15 行创建）的数组上运行。与 LINQ to Objects 一样，PLINQ 版本的这些操作 *不会修改* 原始集合。我们对操作进行计时，以显示 PLINQ（使用多个核心）相对于 LINQ to Objects（使用单个核心）的显著性能改进。在本讨论的剩余部分中，我们将 LINQ to Objects 简称为 LINQ。

```
~~~csharp
// Fig. 19.9: ParallelizingWithPLINQ.cs
// Comparing performance of LINQ and PLINQ Min, Max and Average methods.
using System;
using System.Linq;

class ParallelizingWithPLINQ
{
   static void Main()
   {
      var random = new Random();

      // create array of random ints in the range 1-999
      int[] values = Enumerable.Range(1, 10000000)
         .Select(x => random.Next(1, 1000))
         .ToArray();

      // time the Min, Max and Average LINQ extension methods
      Console.WriteLine(
         "Min, Max and Average with LINQ to Objects using a single core");
      var linqStart = DateTime.Now; // get time before method calls
      var linqMin = values.Min();
      var linqMax = values.Max();
      var linqAverage = values.Average();
      var linqEnd = DateTime.Now; // get time after method calls

      // display results and total time in milliseconds
      var linqTime = linqEnd.Subtract(linqStart).TotalMilliseconds;
      DisplayResults(linqMin, linqMax, linqAverage, linqTime);

      // time the Min, Max and Average PLINQ extension methods
      Console.WriteLine(
         "Min, Max and Average with PLINQ using multiple cores");
~~~
```

**图 19.9** 比较 LINQ 和 PLINQ Min、Max 和 Average 方法的性能。（第 1 部分，共 2 部分。）

```
var plinqStart = DateTime.Now; // get time before method calls
var plinqMin = values.AsParallel().Min();
var plinqMax = values.AsParallel().Max();
var plinqAverage = values.AsParallel().Average();
var plinqEnd = DateTime.Now; // get time after method calls

// display results and total time in milliseconds
var plinqTime = plinqEnd.Subtract(plinqStart).TotalMilliseconds;
DisplayResults(plinqMin, plinqMax, plinqAverage, plinqTime);

// display time difference as a percentage
Console.WriteLine("\nPLINQ took " +
    $"{(plinqTime - linqTime) / linqTime:P0}" +
    " less time than LINQ");
}

// displays results and total time in milliseconds
static void DisplayResults(
    int min, int max, double average, double time)
{
    Console.WriteLine($"Min: {min}\nMax: {max}\n" +
        $"Average: {average:F}\nTotal time in milliseconds: {time:F}");
}
```

使用单个核心的 LINQ to Objects 中的 Min、Max 和 Average
最小值: 1
最大值: 999
平均值: 499.96
总时间（毫秒）: 179.03

使用多个核心的 PLINQ 中的 Min、Max 和 Average
最小值: 1
最大值: 999
平均值: 499.96
总时间（毫秒）: 80.99

PLINQ 比 LINQ 少用了 55 % 的时间

使用单个核心的 LINQ to Objects 中的 Min、Max 和 Average
最小值: 1
最大值: 999
平均值: 500.07
总时间（毫秒）: 152.13

使用多个核心的 PLINQ 中的 Min、Max 和 Average
最小值: 1
最大值: 999
平均值: 500.07
总时间（毫秒）: 89.05

PLINQ 比 LINQ 少用了 41 % 的时间

图 19.9 | 比较 LINQ 和 PLINQ Min、Max 和 Average 方法的性能。（第 2 部分，共 2 部分。）

## 使用 Enumerable 方法 Range 生成 int 范围

使用函数式技术，第 13–15 行创建了一个包含 10,000,000 个随机 ints 的数组。类 Enumerable 提供静态方法 Range 以生成包含整数值的 `IEnumerable<int>`。表达式

```
Enumerable.Range(1, 10000000)
```

生成一个包含 1 到 10,000,000 的值的 `IEnumerable<int>`——第一个参数指定范围中的起始值，第二个参数指定要生成的值的数量。接下来，第 14 行使用 LINQ 扩展方法 `Select` 将每个元素映射到 1–999 范围内的随机整数。lambda

```
x => random.Next(1, 1000)
```

忽略其参数（x），并简单地返回一个随机值，该值成为 Select 返回的 `IEnumerable<int>` 的一部分。最后，第 15 行调用扩展方法 `ToArray`，它返回一个包含 Select 操作生成的元素的 ints 数组。请注意，类 Enumerable 还提供扩展方法 `ToList` 以获取 `List<T>` 而不是数组。

## 使用 LINQ 的 Min、Max 和 Average

要计算 LINQ Min、Max 和 Average 扩展方法调用所需的总时间，我们使用类型 DateTime 的 Now 属性在 LINQ 操作之前（第 20 行）和之后（第 24 行）获取当前时间。第 21–23 行对数组 values 执行 Min、Max 和 Average。第 27 行使用 DateTime 方法 Subtract 计算结束时间和开始时间之间的差异，该差异作为 TimeSpan 返回。然后我们存储 TimeSpan 的 TotalMilliseconds 值，以便在稍后显示 PLINQ 相对于 LINQ 的百分比改进时使用。

## 使用 PLINQ 的 Min、Max 和 Average

第 33–41 行执行与第 20–28 行相同的任务，但使用 PLINQ Min、Max 和 Average 扩展方法调用来演示相对于 LINQ 的性能改进。为了启动并行处理，第 34–36 行调用 IEnumerable<T> 扩展方法 AsParallel（来自类 ParallelEnumerable），它返回一个 ParallelQuery<T>（在此示例中，T 为 int）。实现 ParallelQuery<T> 的对象可与 PLINQ 的并行化 LINQ 扩展方法版本一起使用。类 ParallelEnumerable 定义 ParallelQuery<T>（PLINQ）并行化版本以及几个 PLINQ 特定的扩展方法。有关类 ParallelEnumerable 中定义的扩展方法的更多信息，请访问

```
https://msdn.microsoft.com/library/system.linq.parallelenumerable
```

## 性能差异

第 44–46 行计算并显示 PLINQ 相对于 LINQ 的处理时间百分比改进。如您从示例输出中可以看到，简单选择 PLINQ（通过 AsParallel）大幅降低了总处理时间——在两个示例输出中分别减少了 55% 和 41% 的时间。我们多次运行该应用程序（使用多达三个核心），处理时间节省通常在 41–55% 范围内——尽管我们在一次示例执行中获得了 61% 的节省。总体节省将受到处理器核心数量以及计算机上正在运行的其他内容的影响。

### 数组中的逆变

之前，我们展示了派生类类型的数组（SalariedEmployees）可以分配给基类类型的数组变量（Employees）。现在，考虑以下语句，该语句在 C# 中一直可以编译：

```csharp
SalariedEmployee[] salariedEmployees2 =
    (SalariedEmployee[]) employees;
```

根据之前的语句，我们知道 Employee 数组变量 employees 当前引用的是 SalariedEmployees 的数组。使用强制转换运算符将 employees——基类类型元素的数组——分配给 salariedEmployees2——派生类类型元素的数组——是逆变的一个示例。如果 employees 不是 SalariedEmployees 的数组，前面的强制转换将在运行时失败。

### 泛型类型中的逆变

要了解泛型类型中的逆变，请考虑 SalariedEmployees 的 SortedSet。类 SortedSet<T> 维护按排序顺序排列的对象集——不允许重复。将对象放入 SortedSet 中时，必须实现 IComparable<T> 接口。对于未实现此接口的类，您仍可使用实现 IComparer<T> 接口的对象来比较其对象。此接口的 Compare 方法比较其两个参数，如果相等则返回 0，如果第一个对象小于第二个则返回负整数，如果第一个对象大于第二个则返回正整数。

我们的 Employee 层次结构类未实现 IComparable<T>。假设我们希望按社会安全号码对 Employees 进行排序。我们可以实现以下类来比较任意两个 Employees：

```csharp
class EmployeeComparer : IComparer<Employee>
{
    int IComparer<Employee>.Compare(Employee a, Employee b)
    {
        return a.SocialSecurityNumber.CompareTo(
            b.SocialSecurityNumber);
    }
}
```

方法 Compare 返回使用字符串方法 CompareTo 比较两个 Employees 社会安全号码的结果。

现在考虑以下语句，该语句创建了一个 SortedSet：

```csharp
SortedSet<SalariedEmployee> set =
    new SortedSet<SalariedEmployee>(new EmployeeComparer());
```

当类型参数未实现 IComparable<T> 时，您必须提供适当的 IComparer<T> 对象来比较将放入 SortedSet 中的对象。由于我们正在创建 SalariedEmployees 的 SortedSet，编译器期望 IComparer<T> 对象实现 IComparer<SalariedEmployee>。相反，我们提供了一个实现 IComparer<Employee> 的对象。编译器允许我们在期望派生类类型 IComparer 时提供基类类型的 IComparer，因为接口 IComparer<T> 支持逆变。
