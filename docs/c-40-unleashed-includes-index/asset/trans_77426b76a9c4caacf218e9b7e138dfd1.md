

在没有受检异常（如 Java 中那样）的情况下，一个好的做法是记录委托的“异常契约”（如果有的话）。这样，调用方就能知道他们应该准备处理哪些异常，而实例化委托的一方则应确保引用一个符合这些规则的方法：

```
/// <summary>实现引擎的运行过程。</summary>
/// <exception cref="OutOfFuelException">当燃料耗尽时引发。</exception>
delegate void EngineRunner();
```

一个使用 `EngineRunner` 来运行引擎过程的通用引擎控制器，现在就知道它应该适当地处理 `OutOfFuelException`，而引擎的制造商也知道，在报告这种特定异常错误条件时，应使用该特定异常类型。

在底层，委托的调用不过是对 `Invoke` 实例方法的调用。由此可能产生的一个特殊异常情况是委托对象为 null 引用：

```
Action ouch = null;
ouch(); // 抛出 NullReferenceException
```

换句话说，在适当的地方使用 null 检查来防止此类情况，除非你绝对确定存在非 null 的委托实例（例如，因为之前已经做过 null 检查）。

在图 17.12 中，展示了以下方法中发生的委托调用，并说明了底层 `Invoke` 方法的调用过程：

```
static int Calculate(Func<int, int, int> op, int a, int b) {
    return op(a, b);
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_831_0.png)

图 17.12 委托调用的展开。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_833_0.png)

图 17.13 可扩展的计算器。

除了加、减、乘、除和取模等典型算术运算外，还提供了四个可编程的函数键。编程的方式你可以尽情想象，但更有趣的是如何创建一个通用的计算器引擎，使这些自定义操作能够插入其中。

让我们尝试定义一个 `Calculator` 类来提供核心计算器引擎：

```
class Calculator {
    public int Add(int a, int b) { return a + b; }
    public int Sub(int a, int b) { return a - b; }
    public int Mul(int a, int b) { return a * b; }
    public int Div(int a, int b) { return a / b; }
    public int Mod(int a, int b) { return a % b; }
}
```

这第一次尝试的问题很明显：除了从 `Calculator` 类派生并为想要的新函数提供方法之外，它不允许插入自定义函数。但这本身会引发一个更大的问题：计算器的 UI 如何轻松发现这些新操作？

不仅如此，给定上述 `Calculator` 定义，你如何实现一个求值器？假设用户输入以下按键序列：

1, 2, +, 3, 4, =

根据为操作选择的键（示例中的 +），按下求值按钮 = 需要调用其中一个内置函数。换句话说，你必须使用某种大型多路分支来调用正确的方法（例如，`Add`）。

你可以做得更好，并采用更函数式的方法。如果你基于一个将操作助记符（如 +）映射到相应实现函数的字典来实现计算器，会怎么样？

```csharp
class Calculator {
    private Dictionary<string, Func<int, int, int>> _ops =
        new Dictionary<string, Func<int, int, int>> {
            { "Add", (a, b) => a + b },
            { "Sub", (a, b) => a - b },
            { "Mul", (a, b) => a * b },
            { "Div", (a, b) => a / b },
            { "Mod", (a, b) => a % b }
        };

    public int Eval(int lhs, string op, int rhs) {
        return _ops[op](lhs, rhs);
    }
}
```

`_ops` 字段使用集合初始化器进行初始化，将预编程运算符的键名映射到用于该运算符计算的函数。这个表可以使用 lambda 表达式非常简洁地构建。

现在 `Eval` 方法变得相当简单。给定左侧和右侧操作数以及运算符的友好名称，它通过字典的索引器查找该运算符的实现。获得委托后，它使用委托调用语法调用它。图 17.14 展示了 `Eval` 内部委托查找和调用的逐步求值过程。

为了说明如何实现此计算器之上的 UI，请考虑以下控制台应用程序代码：

```csharp
class CalculatorUI {
    public static void Main() {
        var calc = new Calculator();
        while (true) {
            Console.WriteLine("操作数 1: ");
            int lhs = int.Parse(Console.ReadLine());

            Console.WriteLine("运算符: ");
            string op = Console.ReadLine();

            Console.WriteLine("操作数 2: ");
            int rhs = int.Parse(Console.ReadLine());

            Console.WriteLine("{0}({1},{2}) = {3}", op, lhs, rhs,
                calc.Eval(lhs, op, rhs));
        }
    }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_835_0.png)

图 17.14 运算符委托的表驱动查找。

我们邀请你让这段代码更健壮，以防止用户提供无效的整数字符串（提示：使用 `TryParse`）或无效的运算符名称（提示：在 `Calculator` 上公开某种 `IsValidOperator` 方法，使用内部的 `_ops` 字典）。

剩下的问题是如何让类的用户从外部轻松扩展计算器。答案相当直白。我们只需提供一种方法，将条目添加到封装在 `Calculator` 内部的运算符字典中：

```
class Calculator {
    ...
    public void AddOperator(string name, Func<int, int, int> function) {
        _ops[name] = function;
    }
}
```

例如，计算器的编程接口（无论它可能是什么样子）可以允许用户创建绑定到 F1 键的自定义函数：

```
Func<int, int, int> pyth = (a, b) => (int)Math.Sqrt(a * a + b * b);
calc.AddOperator("F1", pyth);
```

现在，使用参数 3、F1 和 4 调用 `Eval` 将得到 5，即使用勾股定理，边长为 3 和 4 的直角三角形的斜边。

## 关于计算器编程的哲学思考

在讨论可扩展计算器的开头，我们提到了一种替代设计：使用带有虚方法的基础类型 `Calculator` 来处理 F1 到 F4 函数键。自定义计算器将涉及创建派生类型、为这些虚方法提供实现，并编译生成的类型。

这种技术可以与可编程芯片（如可擦除可编程只读存储器芯片或 EPROM）的使用相媲美。在这种情况下，高端计算器的制造商采用我们的通用计算器芯片，并在工厂通过对芯片编程来扩展它。这是一项高级任务，普通最终用户无法直接完成。

另一方面，如果你允许计算器存储可执行代码片段来实现自定义函数，你就不再需要派生自定义计算器类型并编译它来创建高级计算器。相反，你提供一种方法，让通用计算器的最终用户通过调用 `AddOperator` 方法来扩展其功能。

再次将其与物理计算器设备进行比较，这对应于使用带有可编程存储器和小型语言（用于表达自定义函数）的芯片。现在，计算器的最终用户拥有了扩展它的全部灵活性，而无需处理 EPROM 芯片之类的麻烦。

要使你的小计算器在运行时真正可被最终用户扩展，你需要提供一种微型算术语言，允许用户以文本片段的形式输入函数，例如 (a, b) => a * a + b * b。给定这个字符串形式的函数定义，然后你可以在运行时将其编译为委托，这比动态派生专门的 `Calculator` 子类型要可行得多。在第 22 章中，你将学习如何使用表达式树在运行时生成委托。

## 案例研究：LINQ to Objects 中使用的委托

虽然我们将关于 LINQ 的更深入讨论推迟到第 19 章，但我认为花一点时间说明委托在 LINQ 上下文中的使用是值得的。语言集成查询的内置“提供程序”之一允许查询内存中的数据序列，称为 LINQ to Objects。

各种查询运算符被实现为方法，这些方法将 `IEnumerable<T>` 序列作为其输入之一，通常返回一个派生的序列作为结果。这些运算符构成了构建更复杂查询的构建块。换句话说，这些查询运算符允许丰富的组合，这在很大程度上是因为它们受函数式启发的本质。让我们先在图 17.15 中示意性地说明这一点。

