
## 回到过去

有时通过回到 C# 的早期阶段来回顾，能更好地了解我们走了多远。想象一下在 C# 1.0 上实现 LINQ（假设为了演示目的我们已经有了泛型）；前面的查询会是什么样子？对于 Where 过滤器的每一次使用（或其他依赖于委托作为参数的查询运算符），我们都必须引入另一个方法来表达该函数。显然，随着所有方面分散在许多方法中，你的查询将不再可读。

C# 中的 lambda 表达式不仅可以包含表达式体（箭头标记右侧的部分），还可以包含语句体。一个例子是使用 lambda 语法创建 ThreadStart 委托：

```csharp
static void DoBackgroundWork(int nTimes, Action<int> doWork) {
    new Thread(() => {
        for (int i = 0; i < nTimes; i++)
            doWork(i);
    }).Start();
}
```

如果要向 lambda 体传递空参数列表，则需要一对空括号。前述代码中更重要的是，我们在 lambda 表达式的主体内部使用了语句。这里展示的语法在我们使用 C# 2.0 的内联委托语法（使用 delegate 关键字而不是 => 标记）时，最终会归结为相同的 IL 代码。

## C# 中的函数式技术：柯里化

函数式语言通常提供一种按部分应用函数、一次一个参数的方式。这种技术被称为柯里化，以数学家 Haskell Curry 命名（Haskell 编程语言也是以他命名），尽管真正提出这一想法的是 Schönfinkel。

例如，在 F# 中，你可以按如下方式编写一个加法函数：

```fsharp
let add a b = a + b
let addFive = add 5
let seven = addFive 2
```

第二行引起了我们的兴趣：在这里我们调用 add 函数而没有第二个参数。这样做的结果是一个单参数函数，当它被应用到一个参数时，会给它加上 5。这在概念上是通过在 add 函数体内部简单地将 a 替换为 5 来完成的。因此，前面的代码等价于

```fsharp
let addFive =
fun b -> 5 + b (* lambda syntax in F# uses a fun keyword *)
let seven = addFive 2
```

在这种柯里化的设定下，每个函数一次只接受一个参数。因此 add 函数不会同时接受 a 和 b，而是先对 add 应用 a，从而得到一个剩余函数，该函数会消耗 b。例如，下面的伪代码逐步展示了 3 是如何求值的：

```fsharp
let three = (add 1) 2      (* application is left-associative *)
          = (fun b -> 1 + b) 2
          = 1 + 2 = 3
```

换句话说，用 C# 的术语来说，add 的签名不是如下所示：

```csharp
delegate int BinOp(int a, int b);   // Same as Func<int, int, int>
```

而是使用 Func 泛型委托类型，如下所示：

```csharp
Func<int, Func<int, int>>
```

外层的 Func<T1, TResult> 委托类型将 int 作为输入，对应于 a 参数，并返回一个 Func<int, int> 委托。这将是剩余函数，它将 b 参数带入最终结果。

我们如何在 C# 中编写它？使用嵌套的 lambda 表达式：

```csharp
Func<int, Func<int, int>> add = a => b => a + b; // same as a => (b => a + b)
var three = add(1)(2);  // add(1) returns (b => 1 + b) which gets called with 2
var addFive = add(5);   // add(5) returns (b => 5 + b)
var seven = addFive(2); // addFive(2) returns 5 + 2 = 7
```

很漂亮，但由于泛型委托声明，相当冗长。不要担心：很可能你永远不需要编写这样的代码。

## 表达式树

![](img/a16f85e62ce9bdc527f4b09dbfe26092_826_0.png)

如前所述，lambda 表达式作为 C# 3.0 LINQ 语言特性浪潮的一部分被引入，但不仅仅是为了简化创建匿名函数的语法。LINQ 的关键承诺之一是能够使用相同的语言集成语法表达查询，无论它在何处执行。这意味着查询可以针对使用 LINQ to Objects 的内存中对象图，也可以针对使用 LINQ to SQL 或 Entity Framework 的远程数据源，例如 SQL 数据库。

然而，像 SQL Server 这样的数据库不能用代表要执行的查询的 IL 代码来处理，这里完全忽略 SQL CLR 的概念：它们都使用自己的

## LAMBDA 这个名字从何而来？

你可能会想，突然之间，为什么用一个希腊字母来命名一个新的语言特性。Lambda 表达式基于 lambda 演算的概念，这是由 Alonzo Church 在 1920 年代创建的关于数学计算的理论。第一个引入以其命名的特性的语言是 LISP（1958 年），其语言中甚至有一个 LAMBDA 关键字，用来表示类似于如今 C# lambda 表达式的东西。

这再次说明所有好主意都来自数学，尽管它们出现在广泛使用的编程语言中需要一段时间。

## 调用委托

创建委托实例以引用特定方法是为了通过委托调用这些方法的必要步骤。顺便说一下，我们已经展示了如何重复进行此类调用的方法：它们看起来就像普通的函数调用。例如：

```csharp
Func<int, int, int> add = (a, b) => a + b;
int three = add(1, 2);
```

Visual Studio 中的 IntelliSense 显然会通过显示预期参数来帮助调用者。请注意，这些参数的名称来自正在使用的委托类型。在前面的示例中，我们使用的是泛型 Func 类型之一，其中参数的名称类似于 arg1 和 arg2。这在 Visual Studio 中的外观如 17.10 图所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_828_0.png)

图 17.10 调用委托感觉就像调用方法。

当委托按引用传递参数或作为输出时，在调用站点指定参数时必须使用这些修饰符。这与直接调用此类方法的方式完全相似：

```csharp
// delegate string Foo(int a, ref double b, out long c, params DateTime[] ds);
Foo f = /* got it somehow */;
int a = 10;
double d = 12.34;
long c;
string res = f(a, ref d, out c, DateTime.Now);
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_829_0.png)

C# 4.0 引入了命名参数和可选参数的概念，正如我们在讨论方法时之前看到的那样。这两个特性也可以在委托的上下文中使用。让我们先从命名参数开始：

```csharp
Func<int, int, int> add = (a, b) => a + b;
int three = add(arg2: 2, arg1: 1);
```

同样，这些名称来自委托的参数列表，而不是委托所引用的方法。如果你仔细想想，这完全有道理，因为编译器无法确定目标方法的参数列表是什么样子的：

```csharp
static int Calculate(Func<int, int, int> op, int a, int b) {
    return op(a, b);
}
```

```csharp
static void Main() {
    int three = Calculate((x, y) => x + y, 1, 2);
    int eight = Calculate((l, r) => l * r, 2, 4);
}
```

在前面的示例中，传递给 Calculate 的 operator `op` 参数由两个 lambda 表达式提供，一个用于加法，一个用于乘法，每个表达式对其参数使用不同的名称。在委托被调用时，很明显编译器并不知道这些信息。

## 不要在公共 API 中重命名参数

就像常规方法一样，按名称传递参数的能力意味着在向客户发布公共 API 后不应重命名参数。更改参数的名称将在重新编译他们的代码时破坏调用：上次有一个名为 x 的参数，但现在它消失了。如果不重新编译，现有的代码将继续工作，因为命名参数只是编译时特性。在底层生成的 IL 代码中，参数按调用目标所期望的顺序传递。换句话说，运行时不关心参数如何命名：只有它们的顺序重要。

除了在委托的调用站点使用命名参数外，委托还可以使用以下熟悉的语法声明为具有可选参数：

```csharp
delegate void Printer(string message = "");
```

使用它，你可以引用任何接受字符串类型参数的方法，但在通过委托进行调用时，可以省略 message 参数，从而
