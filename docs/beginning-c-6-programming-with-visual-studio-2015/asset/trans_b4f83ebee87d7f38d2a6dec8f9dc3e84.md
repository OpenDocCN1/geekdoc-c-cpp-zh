
```
}
}
WriteLine();
}
```

在 Main() 方法中，你创建了三个 lambda 表达式并依次使用它们调用 PerformOperations()。其中第一个调用如下：

```
WriteLine($"(a, b) = a + b;");
PerformOperations((paramA, paramB) => paramA + paramB);
```

该处使用的 lambda 表达式如下：

```
(paramA, paramB) => paramA + paramB
```

再次，这可以分解为三个部分：

- 1. 参数定义部分。这里有两个参数，paramA 和 paramB。这些参数是无类型的，意味着编译器可以根据上下文推断这些参数的类型。在本例中，编译器可以确定 PerformOperations() 方法调用需要 TwoIntegerOperationDelegate 类型的委托。此委托类型有两个 int 参数，因此通过推断 paramA 和 paramB 均被键入为 int 变量。
- 2. => 运算符。它将 lambda 表达式参数与 lambda 表达式主体分隔开。
- 3. 表达式主体。它指定了一个简单操作，即 paramA 和 paramB 的求和。请注意，无需指定这是一个返回值。编译器知道为了创建一个可与 TwoIntegerOperationDelegate 一起使用的方法，该方法必须具有 int 的返回类型。因为指定的操作 paramA + paramB 的计算结果为 int，且未提供额外信息，编译器推断该表达式的结果应为该方法的返回类型。

然后用长格式书写，你可以将使用此 lambda 表达式的代码扩展为以下使用匿名方法 的代码：

```
WriteLine($"(a, b) = a + b;");
PerformOperations(delegate(int paramA, int paramB)
{
    return paramA + paramB;
});
```

剩余的代码以相同的方式使用两个不同的 lambda 表达式执行操作：

```
WriteLine();
WriteLine($"(a, b) = a * b;");
PerformOperations((paramA, paramB) => paramA * paramB);
WriteLine();
WriteLine($"(a, b) = (a - b) % b;");
PerformOperations((paramA, paramB) => (paramA - paramB)
    % paramB);
ReadKey();
```

之前的示例展示了具有 void 返回类型的委托对语句主体中使用的代码要求不那么严格：

```
myTimer.Elapsed += (source, e) => WriteLine("Event handler called after " +
    $"{(source as Timer).Interval} milliseconds.");
```

这里，语句不求值任何内容，因此它只是被执行，而在任何地方都不使用返回值。

鉴于 lambda 表达式可以被视为匿名方法语法的扩展，你可能不会感到惊讶地得知你也可以将多个语句作为 lambda 表达式语句主体包含在内。为此，你只需提供用大括号括起来的代码块，就像在 C# 中必须提供多行代码的任何其他情况一样：

```
(param1, param2) =>
{
    // Multiple statements ahoy!
}
```

如果将 lambda 表达式与具有非 void 返回类型的委托类型结合使用，则必须使用 return 关键字返回一个值，就像任何其他方法一样：

```
(param1, param2) =>
{
    // Multiple statements ahoy!
    return returnValue;
}
```

例如，之前你看到如何重写 Try It Out 中的以下代码，

```
PerformOperations((paramA, paramB) => paramA + paramB);
```

为：

```
PerformOperations(delegate(int paramA, int paramB)
{
    return paramA + paramB;
});
```

或者，你也可以按如下方式重写代码：

```
PerformOperations((paramA, paramB) =>
{
    return paramA + paramB;
});
```

这更符合原始代码，因为它保持了 paramA 和 paramB 参数的隐式类型。

在大多数情况下，lambda 表达式在使用单表达式时最有用——也最优雅。老实说，如果你需要多个语句，你的代码

## Lambda 表达式与集合

现在你已经了解了 Func<> 泛型委托，你可以理解 System.Linq 命名空间为数组类型提供的一些扩展方法（你在编码过程中可能在 IntelliSense 中看到过它们）。例如，有一个名为 Aggregate() 的扩展方法，其定义了三个重载如下：

```
public static TSource Aggregate<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, TSource, TSource> func);
public static TAccumulate Aggregate<TSource, TAccumulate>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func);
public static TResult Aggregate<TSource, TAccumulate, TResult>(
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func,
    Func<TAccumulate, TResult> resultSelector);
```

与前面显示的扩展方法一样，这乍一看似乎难以理解，但如果你将其分解，就能很容易地弄明白。该函数的 IntelliSense 告诉你它执行以下操作：

> 在序列上应用累加器函数。

这意味着累加器函数（你可以用 lambda 表达式的形式提供）将从头到尾应用于集合中的每个元素。此累加器函数必须有两个参数和一个返回值。一个输入是当前元素；另一个输入是种子值、集合中的第一个值，或前一次求值的結果。

在三个重载中最简单的重载中，只有一个泛型类型规范，可以从实例参数的类型推断出来。例如，在以下代码中，泛型类型规范将为 int（累加器函数暂时留空）：

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate(...);
```

这等同于以下内容：

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate<int>(...);
```

这里所需的 lambda 表达式可以从扩展方法规范推断出来。因为在此代码中类型 TSource 为 int，所以你必须为委托 Func<int, int, int> 提供一个 lambda 表达式。例如，你可以使用之前见过的：

```
int[] myIntArray = { 2, 6, 3 };
int result = myIntArray.Aggregate((paramA, paramB) => paramA + paramB);
```

此调用导致 lambda 表达式被调用两次，首先 paramA = 2 且 paramB = 6，然后 paramA = 8（第一次计算的结果）且 paramB = 3。最终结果

分配给变量 result 的值为 int 值 11——数组中所有元素的总和。

Aggregate() 扩展方法的另外两个重载类似，但使你能够执行稍微复杂一些的处理。这在下面的简短 Try It Out 中有所说明。

## 试一试 使用 Lambda 表达式与集合：Ch13Ex09\Program.cs

- 1. 创建一个新的控制台应用程序，命名为 Ch13Ex09，并将其保存在目录 C:\BegVCSharp\Chapter13 中。
- 2. 按如下方式修改 Program.cs 中的代码：
- 3. 运行应用程序。结果如图 13-21 所示。

```csharp
static void Main(string[] args)
{
    string[] curries = { "pathia", "jalfrezi", "korma" };
    WriteLine(curries.Aggregate(
        (a, b) => a + " " + b));
    WriteLine(curries.Aggregate<string, int>(
        0,
        (a, b) => a + b.Length));
    WriteLine(curries.Aggregate<string, string, string>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a));
    WriteLine(curries.Aggregate<string, string, int>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a.Length));
    ReadKey();
}
```

![](img/cf72ea860016d2d680fc085fc06f265a_427_0.png)

## 工作原理

在此示例中，你使用包含三个元素的字符串数组作为源数据，对 Aggregate() 扩展方法的每个重载进行了实验。

首先，执行简单的连接：

```
WriteLine(curries.Aggregate((a, b) => a + " " + b));
```
