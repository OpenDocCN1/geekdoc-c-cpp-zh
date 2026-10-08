

## 21.11 使用 LINQ 方法调用语法和 Lambda 进行函数式编程

函数式编程的一个关键方面是不可变性——即不修改正在处理的数据源或任何其他程序状态（例如循环中的计数变量）。通过使用内部迭代，你可以消除程序中因不正确修改数据而引起的常见错误。这使得编写正确的代码变得更容易。

## Filter、Map 和 Reduce

你在数据集合上执行的三个常用函数式编程操作是 filter（过滤）、map（映射）和 reduce（归约）：

- filter 操作产生一个新的集合，其中仅包含满足条件的元素。例如，你可能过滤一个整数集合以只找到偶数，或者对员工集合进行过滤以只找到某大公司特定部门的员工。Filter 操作不会修改原始集合。

- map 操作产生一个新的集合，其中原始集合中的每个元素都映射到一个新值（可能类型不同）——例如，将数值映射到这些数值的平方。新集合的元素数量与被映射的集合相同。Map 操作不会修改原始集合。

- reduce 操作使用指定如何合并元素的 lambda 表达式将集合中的元素合并为单个新值。例如，你可能将一个从 0 到 100 的年级集合归约为成绩大于或等于 60 分的学生的枚举数量。Reduce 操作不会修改原始集合。

在下一节中，我们将使用类扩展方法演示 filter、map 和 reduce 操作，分别对应 Select 和 Aggregate。这些扩展方法由类 `Enumerable` 定义，适用于实现了 `IEnumerable<T>` 接口的集合上。

## C# 与函数式编程

尽管 C# 最初并非被设计为函数式编程语言，但 C# 的查询语法和 LINQ 扩展方法支持函数式编程技术，例如内部迭代和不可变性。此外，C# 6 的只读 getter 自动实现属性使得定义不可变类型变得更容易。我们预计 C# 以及大多数其他流行编程语言未来将包含更多函数式编程能力，使以函数式风格实现程序变得更加自然。

## 21.11 使用 LINQ 方法调用语法和 Lambda 进行函数式编程

在第 9 章中，我们引入了 LINQ，演示了 LINQ 查询语法并引入了一些 LINQ 扩展方法。你使用 LINQ 查询语法执行的任务也可以通过各种 LINQ 扩展方法和 lambda 完成。事实上，编译器会将 LINQ 查询翻译为对 LINQ 扩展方法的调用，并接收 lambda 作为参数。例如，图 9.2 的第 21–24 行

```csharp
var filtered =
  from value in values // 数据源是
  where value > 4
  select value;
```

可以写为：

```csharp
var filtered = values.Where(value => value > 4);
```

图 21.8 展示了使用整数列表的简单函数式编程技术。

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

在整个示例中，我们通过调用扩展方法来显示各种操作的结果，该扩展方法定义在静态类 `Extensions` 中。在 Main 的开始和结束，我们对 `IEnumerable<T>` 参数调用 `Display` 以按顺序显示元素。

## 21.11.1 LINQ 扩展方法：Min, Max, Sum 和 Average

类 `Enumerable` 定义了用于执行常见操作的各种 LINQ 扩展方法：

- Min（第19行）返回集合中的最小值。
- Max（第20行）返回集合中的最大值。
- Sum（第21行）返回所有值的总和。
- Average（第22行）返回所有值的平均值。

## 迭代和变异对你是隐藏的

事实上，LINQ 操作没有修改原始集合或应用程序中任何变量的副作用——

- 我们只需说想要实现什么，而不是*如何*实现。
- values 集合*没有被修改*（由第52行证实）。

当然，在后台需要迭代和可变变量：

- 所有四个扩展方法都会遍历集合并跟踪当前元素。
- 在遍历集合时，Min 和 Average 分别存储当前的极值，而 Sum 和 Average 必须跟踪已处理元素的总和——这些操作都会修改局部变量。

21.11.2 到21.11.4节中的其他操作也需要迭代和可变变量，但*库*（已经过调试和测试）为你处理了这些细节。要查看 Min、Max、Sum 和 Average 等 LINQ 扩展方法如何实现这些概念，请查看 .NET 源码中的 Enumerable：

```
https://github.com/dotnet/corefx/tree/master/src/System.Linq/src/System/Linq
```

## 21.11.2 用于归约操作的 Aggregate 扩展方法

你可以使用 *Aggregate* LINQ 方法定义归约。例如，第25–26行的 Aggregate 调用对 values 的元素求和。这里使用的 Aggregate 版本接收两个参数：

- 第一个参数（0）是帮助你开始归约操作的值。在对集合求和时，从 0 开始。很快我们将使用 1 开始计算元素的乘积。
- 第二个参数是类型为 *Func*（命名空间）的委托，表示一个接收两个相同类型参数并返回一个值的方法——有许多 *Func* 版本可以指定从 0 到 16 个任意类型的参数。

