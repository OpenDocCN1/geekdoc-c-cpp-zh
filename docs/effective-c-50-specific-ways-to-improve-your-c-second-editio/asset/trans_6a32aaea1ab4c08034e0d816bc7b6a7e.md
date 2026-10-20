

已知的方法是可用的。这在你想要创建一个依赖于某个运算符（如 +）的通用方法时尤其受限。动态调用可以解决这个问题。只要成员在运行时可用，就可以使用它。下面是一个方法，它可以对两个动态对象进行加法，只要在运行时有可用的 + 运算符：

```
public static dynamic Add(dynamic left,
    dynamic right)
{
    return left + right;
}
```

这是我第一次讨论 dynamic，所以让我们看看它在做什么。Dynamic 可以被认为是“带有运行时绑定的 System.Object”。在编译时，dynamic 变量只有 System.Object 中定义的方法。然而，编译器会添加代码，使得每次成员访问都被实现为一个动态调用站点。在运行时，代码会执行以检查对象并确定请求的成员是否可用。（参见第 41 条关于实现动态对象。）这通常被称为“鸭子类型”：如果它走起来像鸭子，说起来像鸭子，那它也就可以被当作鸭子。你不需要声明特定的接口，或提供任何编译时类型操作。只要在运行时需要的成员可用，它就会工作。

对于上面的这个方法，动态调用站点将确定对于两个对象实际的运行时类型是否存在可访问的 + 运算符。所有这些调用都会提供一个正确的答案：

```
dynamic answer = Add(5, 5);
answer = Add(5.5, 7.3);
answer = Add(5, 12.3);
```

请注意，answer 必须声明为 dynamic 对象。因为调用是动态的，编译器无法知道返回值的类型。那必须在运行时解析。唯一在运行时解析返回代码类型的方法就是将其设为 dynamic 对象。返回值的静态类型是 dynamic。它的运行时类型在运行时解析。

当然，这个动态 Add 方法并不局限于数值类型。你可以对字符串进行加法（因为 string 确实定义了 + 运算符）：

```
dynamic label = Add("Here is ", "a label");
```

你可以将一个时间跨度加到一个日期上：

```
dynamic tomorrow = Add(DateTime.Now, TimeSpan.FromDays(1));
```

只要有可访问的 + 运算符，动态版本的 Add 就会工作。

这种对 dynamic 的开篇解释可能会让你过度使用动态编程。我只讨论了动态编程的优点。现在是考虑缺点的时候了。你已经离开了类型系统的安全保障，并且因此限制了编译器可以帮助你的方式。任何对类型的解释错误都只能在运行时被发现。

任何操作中其中一个操作数（包括可能的 this 引用）为 dynamic 的结果本身也是 dynamic。在某个时刻，你会希望将这些动态对象带回 C# 代码中使用的静态类型系统。那将需要一个强制转换或转换操作：

```
answer = Add(5, 12.3);
int value = (int)answer;
string stringLabel = System.Convert.ToString(answer);
```

强制转换操作在动态对象的实际类型是目标类型，或可以强制转换为目标类型时有效。你需要知道任何动态操作的正确结果类型才能为其赋予强类型。否则，转换将在运行时失败，抛出异常。

使用 dynamic 类型是在你必须在不知道所涉及类型的情况下在运行时解析方法时正确的工具。当你有编译时知识时，你应该使用 lambda 表达式和函数式编程结构来创建你需要的解决方案。你可以用 lambda 重写 Add 方法，如下所示：

```
public static TResult Add<T1, T2, TResult>(T1 left, T2 right,
    Func<T1, T2, TResult> AddMethod)
{
    return AddMethod(left, right);
}
```

每个调用者都必须提供特定方法。所有之前的示例都可以用这种策略实现：

```
var lambdaAnswer = Add(5, 5, (a, b) => a + b);
var lambdaAnswer2 = Add(5.5, 7.3, (a, b) => a + b);
```

```
var lambdaAnswer3 = Add(5, 12.3, (a, b) => a + b);
var lambdaLabel = Add("Here is ", "a label",
    (a, b) => a + b);
dynamic tomorrow = Add(DateTime.Now, TimeSpan.FromDays(1));
var finalLabel = Add("something", 3,
    (a,b) => a + b.ToString());
```

你可以看到最后一个方法要求你指定从 int 到 string 的转换。它也有一种有点丑的感觉，因为所有那些 lambda 看起来都可以被合并成一个通用方法。不幸的是，这就是这个解决方案的工作方式。你必须在类型可以被推断的位置提供 lambda。这意味着看起来对人类来说相同的大量代码必须被重复，因为对编译器来说代码并不相同。当然，将 Add 方法定义为实现 Add 似乎很愚蠢。实际上，你会将这种技术用于使用 lambda 但不只是执行它的那些方法。它是在 .NET 库 Enumerable.Aggregate() 中使用的技术。Aggregate() 枚举整个序列并通过加法（或执行其他操作）生成单个结果：

```
var accumulatedTotal = Enumerable.Aggregate(sequence,
    (a, b) => a + b);
```

它仍然感觉像你在重复代码。避免这种重复代码的一种方法是使用表达式树。这是在运行时构建代码的另一种方式。System.Linq.Expression 类及其派生类为你提供了构建表达式树的 API。一旦你构建了表达式树，你将其转换为 lambda 表达式并将生成的 lambda 表达式编译成委托。例如，这段代码构建并在三个相同类型的值上执行 Add：

```
// Naive Implementation. Read on for a better version
public static T AddExpression<T>(T left, T right)
{
    ParameterExpression leftOperand = Expression.Parameter(
        typeof(T), "left");
    ParameterExpression rightOperand = Expression.Parameter(
        typeof(T), "right");
    BinaryExpression body = Expression.Add(
        leftOperand, rightOperand);
    Expression<Func<T, T, T>> adder =
        Expression.Lambda<Func<T, T, T>>(
```

```
body, leftOperand, rightOperand);
Func<T, T, T> theDelegate = adder.Compile();
return theDelegate(left, right);
}
```

大部分有趣的工作涉及类型信息，所以与其像我在生产代码中为了清晰会使用 var，我特意为所有类型命名。

前两行为名为“left”和“right”的变量创建参数表达式，两者都是类型 T。下一行使用这两个参数创建 Add 表达式。Add 表达式派生自 BinaryExpression。你应该能够为其他二元运算符创建类似的表达式。

接下来，你需要从表达式体和两个参数构建 lambda 表达式。最后，你通过编译表达式创建 Func<T,T,T> 委托。一旦编译，你可以执行它并返回结果。当然，你可以像调用任何其他泛型方法一样调用它：

```
int sum = AddExpression(5, 7);
```

我在最后一个示例上方添加了注释，指出这是一个天真的实现。不要将此代码复制到你的工作应用程序中。此版本有两个问题。首先，有很多情况它不起作用但 Add() 应该起作用。有几个有效的 Add() 方法的示例接受不相似的参数：int 和 double，DateTime 和 TimeSpan 等。这些方法在此方法中不起作用。让我们修复它。你必须在方法中再添加两个泛型参数。然后，你可以为操作左侧和右侧指定不同的操作数。顺便说一下，我用 var 声明替换了一些局部变量名。这模糊了类型信息，但确实有助于使方法逻辑更清晰。

```
// A little better.
public static TResult AddExpression<T1, T2, TResult>
    (T1 left, T2 right)
{
    var leftOperand = Expression.Parameter(typeof(T1), "left");
    var rightOperand = Expression.Parameter(typeof(T2), "right");
    var body = Expression.Add(leftOperand, rightOperand);
