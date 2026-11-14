

body, leftOperand, rightOperand);
Func<T, T, T> theDelegate = adder.Compile();
return theDelegate(left, right);
}

大部分有趣的工作都涉及类型信息，因此为了清晰起见，我没有在生产代码中像平时那样使用 var，而是明确指定了所有类型。

前两行分别为名为“left”和“right”的变量创建参数表达式，两者类型均为 T。下一行使用这两个参数创建一个 Add 表达式。Add 表达式派生自 BinaryExpression。你应该能够为其他二元运算符创建类似的表达式。

接下来，你需要从表达式体和两个参数构建 lambda 表达式。最后，通过编译表达式创建 Func<T,T,T> 委托。编译后，你可以执行它并返回结果。当然，你可以像调用其他任何泛型方法一样调用它：

```
int sum = AddExpression(5, 7);
```

我在最后一个示例上方添加了注释，表明这是一个简单的实现。请勿将此代码复制到你的工作应用程序中。此版本有两个问题。首先，有很多情况下它不起作用，但 Add() 应该可以工作。有几个有效的 Add() 方法示例接受不同类型的参数：int 和 double、DateTime 和 TimeSpan 等。这些都无法与此方法一起使用。让我们修复它。你必须向方法添加两个额外的泛型参数。然后，你可以在操作的左侧和右侧指定不同的操作数。顺便说一句，我将一些局部变量名替换为 var 声明。这会模糊类型信息，但确实有助于使方法的逻辑更加清晰。

```
// A little better.
public static TResult AddExpression<T1, T2, TResult>
    (T1 left, T2 right)
{
    var leftOperand = Expression.Parameter(typeof(T1),
        "left");
    var rightOperand = Expression.Parameter(typeof(T2),
        "right");
    var body = Expression.Add(leftOperand, rightOperand);
    var adder = Expression.Lambda<Func<T1, T2, TResult>>(
        body, leftOperand, rightOperand);
    return adder.Compile()(left, right);
}
```

此方法与前一个版本非常相似；它只是允许你为左操作数和右操作数使用不同的类型进行调用。唯一的缺点是，每次调用此版本时都需要指定所有三个参数类型：

```
int sum2 = AddExpression<int, int, int>(5, 7);
```

但是，因为你指定了所有三个参数，所以参数类型不同的表达式可以工作：

```
DateTime nextWeek = AddExpression<DateTime, TimeSpan,
DateTime>(
    DateTime.Now, TimeSpan.FromDays(7));
```

是时候解决另一个令人烦恼的问题了。迄今为止我展示的代码，每次调用 AddExpression() 方法时都会将表达式编译为委托。这非常低效，尤其是如果你反复执行同一个表达式。编译表达式代价高昂，因此你应该缓存编译后的委托以供将来调用。以下是该类的初步版本：

```
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
        var rightOperand = Expression.Parameter(typeof(T2),
            "right");
        var body = Expression.Add(leftOperand, rightOperand);
        var adder = Expression.Lambda<Func<T1, T2, TResult>>(
            body, leftOperand, rightOperand);
        compiledExpression = adder.Compile();
    }
}
```

到此，你可能在想该使用哪种技术：dynamic 还是 Expressions。这个决定取决于具体情况。Expression 版本使用了一组稍简单的运行时计算。这在许多情况下可能使其更快。然而，表达式不如 dynamic 调用那么动态。请记住，使用 dynamic 调用时，你可以成功添加许多不同的类型：int 和 double、short 和 float，随便什么。只要在 C# 代码中是合法的，在编译后的版本中也是合法的。你甚至可以添加字符串和数字。如果使用表达式版本尝试相同的场景，任何这些合法的 dynamic 版本都会抛出 InvalidOperationException。尽管存在可行的转换操作，但你构建的 Expressions 并未将这些转换构建到 lambda 表达式中。Dynamic 调用会做更多工作，因此支持更多不同类型的操作。例如，假设你想更新 AddExpression 以添加不同类型并执行适当的转换。好吧，你只需更新构建表达式的代码，以包含从参数类型到结果类型的转换。它看起来如下：

```
// A fix for one problem causes another
public static TResult AddExpressionWithConversion
    <T1, T2, TResult>(T1 left, T2 right)
{
    var leftOperand = Expression.Parameter(typeof(T1),
        "left");
    Expression convertedLeft = leftOperand;
    if (typeof(T1) != typeof(TResult))
    {
        convertedLeft = Expression.Convert(leftOperand,
            typeof(TResult));
    }

    var rightOperand = Expression.Parameter(typeof(T2),
        "right");
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

这将修复所有需要转换的加法问题，例如添加 double 和 int，或者将 double 添加到字符串且结果为字符串。然而，它会破坏参数不应与结果相同的有效用法。特别是，此版本无法用于上面将 TimeSpan 添加到 DateTime 的示例。通过编写大量更多代码，你可以解决这个问题。然而，到那时，你基本上已经重新实现了处理 C# dynamic 分发的代码（参见第 41 条）。与其做所有这些工作，不如直接使用 dynamic。

当操作数和结果相同时，你应该使用表达式版本。这能为你提供泛型类型参数推断，并在代码在运行时失败时减少排列组合。以下是我推荐用于使用 Expression 实现运行时分发的版本：

```
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
        var rightOperand = Expression.Parameter(typeof(T),
            "right");
        var body = Expression.Add(leftOperand, rightOperand);
        var adder = Expression.Lambda<Func<T, T, T>>(
            body, leftOperand, rightOperand);
        compiledExpression = adder.Compile();
    }
}
```

调用 Add 时，你仍然需要指定唯一的类型参数。这样做确实能让你利用编译器在调用点创建任何转换。编译器可以将 int 提升为 double，依此类推。

使用 dynamic 和在运行时构建表达式也存在性能开销。就像任何动态类型系统一样，你的程序在运行时有更多工作要做，因为编译器没有执行其常规的类型检查。编译器必须生成指令来在运行时执行所有这些检查。我不想夸大其词，因为 C# 编译器确实会为运行时检查生成高效的代码。在大多数情况下，使用 dynamic 比编写自己的代码来使用反射并生成自己的后期绑定版本要快。然而，运行时工作量不是零；所花费的时间也不是零。如果你可以使用静态类型来解决问题，它无疑将比使用动态类型更高效。

当你控制所有涉及的类型，并且可以创建接口而不是使用动态编程时，那是更好的解决方案。你可以定义接口，针对接口进行编程，并在所有应表现出接口定义行为的类型中实现该接口。C# 类型系统将使在代码中引入类型错误变得更加困难，编译器会生成更高效的代码，因为它可以假设某些类别的错误是不可能的。

在许多情况下，你可以使用 lambda 创建泛型 API，并强制调用者定义你在动态算法中会执行的代码。

下一个选择是使用表达式。如果你针对不同类型的排列组合数量相对较少，且可能的转换数量也较少，那么这是正确的选择。你可以控制创建哪些表达式，从而控制运行时发生多少工作。

