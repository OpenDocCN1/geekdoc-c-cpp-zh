

```
var adder = Expression.Lambda<Func<T1, T2, TResult>>(
    body, leftOperand, rightOperand);
return adder.Compile()(left, right);
}
```

此方法看起来与之前的版本非常相似；它只是让你可以用左右操作数的不同类型来调用它。唯一的缺点是，每次调用此版本时，你都需要指定全部三个参数类型：

```
```csharp
int sum2 = AddExpression<int, int, int>(5, 7);
```
```

然而，由于你指定了全部三个参数，具有不相似参数的表达式也能工作：

```
```csharp
DateTime nextWeek= AddExpression<DateTime, TimeSpan,
    DateTime>(
    DateTime.Now, TimeSpan.FromDays(7));
```
```

是时候解决另一个令人困扰的问题了。到目前为止我展示的代码，每次调用 AddExpression() 方法时都会将表达式编译成委托。这相当低效，尤其是如果你反复执行同一个表达式时。编译表达式代价很高，因此你应该为后续调用缓存已编译的委托。下面是该类的第一次尝试：

```
```csharp
// dangerous but working version
public static class BinaryOperator<T1, T2, TResult>
{
    static Func<T1, T2, TResult> compiledExpression;

    public static TResult Add(T1 left, T2 right)
    {
        if (compiledExpression == null)
            createFunc();

        return compiledExpression(left, right);
    }

    private static void createFunc()
    {
        var leftOperand = Expression.Parameter(typeof(T1),
            "left");
```

```
var rightOperand = Expression.Parameter(typeof(T2), "right");
var body = Expression.Add(leftOperand, rightOperand);
var adder = Expression.Lambda<Func<T1, T2, TResult>>(
    body, leftOperand, rightOperand);
compiledExpression = adder.Compile();
}
```

此时，你可能在想该使用哪种技术：dynamic 还是 Expressions。这个决定取决于具体情况。Expression 版本使用了一组稍简单的运行时计算。在许多情况下，这可能会使其更快。然而，表达式比动态调用要少一些动态性。记住，使用动态调用时，你可以成功添加许多不同类型：int 和 double，short 和 float，等等。只要在 C# 代码中合法，在编译版本中就合法。你甚至可以添加字符串和数字。如果你尝试使用表达式版本实现同样的场景，任何这些合法的动态版本都会抛出 InvalidOperationException。即使存在可用的转换操作，你构建的 Expressions 也不会将这些转换构建到 lambda 表达式中。动态调用做了更多工作，因此支持更多不同类型的操作。例如，假设你想更新 AddExpression 以添加不同类型并执行适当的转换。好吧，你只需要更新构建表达式的代码，自己加入从参数类型到结果类型的转换即可。它的样子如下：

```
// A fix for one problem causes another
public static TResult AddExpressionWithConversion<T1, T2, TResult>(T1 left, T2 right)
{
    var leftOperand = Expression.Parameter(typeof(T1), "left");
    Expression convertedLeft = leftOperand;
    if (typeof(T1) != typeof(TResult))
    {
        convertedLeft = Expression.Convert(leftOperand, typeof(TResult));
    }
    var rightOperand = Expression.Parameter(typeof(T2), "right");
```

```
```csharp
Expression convertedRight = rightOperand;
if (typeof(T2) != typeof(TResult))
{
    convertedRight = Expression.Convert(rightOperand,
        typeof(TResult));
}
var body = Expression.Add(convertedLeft, convertedRight);
var adder = Expression.Lambda<Func<T1, T2, TResult>>(
    body, leftOperand, rightOperand);
return adder.Compile()(left, right);
}
```
```

这将修复所有需要转换的加法问题，例如添加 double 和 int，或将 double 加到字符串并结果为字符串。然而，它破坏了参数不应与结果相同时的有效用法。特别是，此版本无法使用上面添加 TimeSpan 到 DateTime 的示例。通过更多代码，你可以解决这个问题。然而，到那时，你基本上已经重新实现了 C# 处理动态分派的代码（参见第 41 条）。与其做所有这些工作，直接使用 dynamic 即可。

你应该在操作数和结果相同时使用表达式版本。这能让你获得泛型类型参数推断，并且在运行时代码失败时排列组合更少。以下是如果使用 Expression 实现运行时分派我会推荐的版本：

```
```csharp
public static class BinaryOperators<T>
{
    static Func<T, T, T> compiledExpression;

    public static T Add(T left, T right)
    {
        if (compiledExpression == null)
            createFunc();

        return compiledExpression(left, right);
    }

    private static void createFunc()
    {
        var leftOperand = Expression.Parameter(typeof(T),
            "left");
```

```
```csharp
var rightOperand = Expression.Parameter(typeof(T),
    "right");
var body = Expression.Add(leftOperand, rightOperand);
var adder = Expression.Lambda<Func<T, T, T>>(
    body, leftOperand, rightOperand);
compiledExpression = adder.Compile();
}
}
```
```

你仍然需要在调用 Add 时指定一个类型参数。这样做的好处是，你可以利用编译器在调用点创建任何转换。编译器可以把 int 提升为 double 等等。

使用 dynamic 和在运行时构建表达式也存在性能成本。就像任何动态类型系统一样，你的程序在运行时需要做更多工作，因为编译器没有执行任何通常的类型检查。编译器必须生成指令在运行时执行所有这些检查。我不想夸大其词，因为 C# 编译器确实为执行运行时检查生成了高效的代码。在大多数情况下，使用 dynamic 会比自己编写代码使用反射并生成自己的后期绑定版本更快。然而，运行时工作量并非为零；所需时间也并非为零。如果你能用静态类型解决一个问题，它无疑会比使用动态类型更高效。

当你控制所有涉及的类型，并且可以用接口代替动态编程时，那是更好的解决方案。你可以定义接口、针对接口编程，并在所有应表现出接口定义行为的类型中实现该接口。C# 类型系统会使在代码中引入类型错误变得更困难，并且编译器会生成更高效的代码，因为它可以假设某些类别的错误是不可能发生的。

在许多情况下，你可以使用 lambda 创建泛型 API，并强制调用者定义你在动态算法中会执行的代码。

下一个选择是使用表达式。如果不同类型的排列组合相对较少，并且可能发生的转换也很少，这是正确的选择。你可以控制创建哪些表达式，因此可以控制运行时发生的多少工作。

当你使用 dynamic 时，底层的动态基础设施会努力让任何可能的合法构造都能工作，无论运行时工作多么昂贵。

然而，对于本文开头我演示的 Add() 方法来说，这是不可能的。Add() 应该在 .NET 类库中已定义的许多类型上工作。你无法回头为这些类型添加 IAdd 接口。你也不能保证你想要工作的所有第三方库都会符合某个新接口。基于特定成员存在来构建方法的最佳方式是编写一个动态方法，将该选择推迟到运行时。动态实现会找到合适的实现，使用它，并为更好的性能进行缓存。它比纯静态类型解决方案更昂贵，但比解析表达式树要简单得多。

## 第 39 条：使用 Dynamic 利用泛型类型参数的运行时类型

System.Linq.Enumerable.Cast<T> 将序列中的每个对象强制转换为目标类型 T。它是框架的一部分，以便 LINQ 查询可以用在 IEnumerable 序列上（而不是 IEnumerable<T>）。Cast<T> 是一个泛型方法，对 T 没有约束。这限制了它可用的转换类型。如果你在使用 Cast<T> 时不了解其限制，你会发现它似乎不起作用。实际上，它正按预期工作，只是与你期望的不同。让我们检查其内部工作原理和限制。然后，很容易创建一个符合你期望的不同版本。

问题的根源在于 Cast<T> 是在没有任何关于 T 的知识的情况下编译成 MSIL 的，除了 T 必须是派生自 System.Object 的托管类型这一事实。因此，它的工作仅使用 System.Object 中定义的功能。检查这个类：

```
public class MyType
{
    public String StringMember { get; set; }

    public static implicit operator String(MyType aString)
    {
        return aString.StringMember;
    }
}
```

