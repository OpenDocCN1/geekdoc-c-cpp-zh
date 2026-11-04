
```csharp
case Color.Green:
    Console.WriteLine("Green grass.");
    break;
case Color.Blue:
    Console.WriteLine("Saw a primary color!");
    break;
}
```

就我个人而言，我很少使用它，甚至根本不用。代码可能在几秒钟内变得相当难以阅读，你最终可能会花很多小时去追踪那些到处跳转的代码。尽量避免使用它。

哪些类型的表达式（在此上下文中称为*控制类型*）可以用于 switch？任何整型（sbyte、byte、short、ushort、int、uint、long、ulong）、bool（你为什么要那样做？）、char 和枚举类型。如果要 switch 的表达式不属于这些类型中的任何一种，则会尝试进行隐式转换，但如果该尝试也不起作用，则会发生编译时错误。

case 标签需要具有编译时常量值，并且这些值全都不同：

```csharp
string john = "John";

switch (name)
{
    case "Bart": // OK.
        // ...
        break;
    case john: // Not OK, unless you would use const string john = "John" instead.
        // ...
        break;
    case "Bart": // Not OK, already have "Bart" case covered.
        // ...
        break;
}
```

C# 中 switch 语句的特性之一是 case 标签的顺序无关紧要。（在 C 和 C++ 中，它确实重要，因为允许贯穿。）这也有助于解释为什么需要编译时常量：如果 case 标签值在运行时可能相同，并且 case 标签的求值顺序未指定，那么代码将以什么顺序执行？此外，想一想如果 case 标签是需要求值的表达式，那么在副作用顺序方面会发生什么。如果你需要检查非常量值或想要强制顺序，if 语句是你的朋友。

当使用枚举作为控制类型时，可能的值是明确定义的。因此，代码编辑器可以变得更加智能。要对一个枚举值进行 switch，并为每个可能的枚举值提供 case，可以使用代码片段（见图 7.7）。

### 1. switch 代码片段的 IntelliSense

![](img/a16f85e62ce9bdc527f4b09dbfe26092_397_0.png)

### 2. 按两次 Tab 并键入 Color

![](img/a16f85e62ce9bdc527f4b09dbfe26092_397_1.png)

### 3. 按 Enter

![](img/a16f85e62ce9bdc527f4b09dbfe26092_397_2.png)

图 7.7 对枚举值进行 switch 的代码片段。

## “完整”的 SWITCH

枚举表示属于同一域的有限已知常量值集合。例如，我们定义了三种颜色，仅此而已。所以从本质上讲，这里展示的 switch 是“完整”的，因为它覆盖了所有可能的值。真的是这样吗？

首先，我们为什么要关心一个 switch 是否具有“完整”这一属性？原因如下：假设你想编写一个函数，为每个可能的情况返回某个值，如下所示：

```csharp
string ToDutchString(Color color)
{
    switch (color)
    {
        case Color.Red:
            return "rood";
        case Color.Green:
            return "groen";
        case Color.Blue:
            return "blauw";
    }
}
```

不幸的是，前面的代码无法编译，因为 C# 编译器没有意识到（有充分理由，继续读下去）我们正在穷尽测试 Color 枚举域中看起来所有的值。因此，它看到存在一条不保证从方法返回字符串的代码路径。我们要么需要提供 default case，要么在方法末尾返回某个虚拟值。或者我们通过抛出异常以强制方式返回：

```
default:
    throw new InvalidOperationException("Unknown color.");
```

如果你正在处理代码覆盖率，这可能会特别烦人，因为似乎不可能命中 default case。如果我们能告诉编译器该 switch 是“完整”的（或者让它推断出来），那岂不是很好？如果枚举类型真的能建立有限域，那确实会很好。但它们不能。

你从枚举的一种用法——标志——中已经知道这一点。在第 5 章中，我们研究了用于测试标志的位级掩码操作。FileMode 的枚举可以将 Read 和 Write 值定义为 2 的幂，允许用户使用按位 | 运算符将它们组合成 ReadWrite。我们刚刚创建了一个也是有效 FileMode 的值，但它不一定在枚举中显式声明过。

但即使不使用标志，枚举也只是伪装的整数。在我们的 Color 定义中，枚举实际上是一个 int，其中一些符号常量使用编译器生成的数字定义（Red = 0、Green = 1 和 Blue = 2）。由于整数表示形式便于作为存储机制（而不是将新值存储为字符串），你可以在枚举及其基础类型之间来回转换：

```
var unknownColor = (Color)4;
```

这就是未知枚举值如何诞生的，有点不幸。

从风格的角度来看，一个经常反复出现的问题是，switch 语句的嵌入语句是否应该用一对花括号括起来。记住，块可以用于作用域目的，因此如果你需要局部状态并且不想污染外部作用域，使用花括号可能是有益的：

```csharp
static int Eval(Expression ex)
{
    switch (ex.NodeType)
    {
        case ExpressionType.Constant:
        {
            var ce = (ConstantExpression)ex;
            if (!(ce.Value is int))
                throw new InvalidOperationException("Only int supported.");
            return (int)ce.Value;
        }
        case ExpressionType.Add:
        {
            var be = (BinaryExpression)ex;
            return Eval(be.Left) + Eval(be.Right);
        }
        case ExpressionType.Multiply:
        {
            var be = (BinaryExpression)ex;
            return Eval(be.Left) * Eval(be.Right);
        }
        // Other binary operations.
        default:
            throw new NotSupportedException("Can't evaluate " + ex + ".");
    }
}
```

这段代码使用 System.Linq.Expressions 命名空间中的表达式树，为数学表达式定义了一个递归表达式求值器。其机制与本次讨论的范围无关（而且真正的求值器肯定会更复杂）。重要的是 case 标签下方使用了块，这使我们能够在不同 case 中重用变量名等。虽然这种编码风格可行，但我不是很喜欢它。

考虑一下：前面的 switch 语句可能会有更多的 case（减法、除法、取余、checked 对应项、一元运算符等），导致包含它的方法变得非常大。这不仅损害代码可读性，还会妨碍“心灵调试”。你的 IT 同事走进办公室，手里拿着一张便签纸上潦草写下的异常堆栈跟踪（如果你在一家现代公司，则发来一封电子邮件）。上面写着 Eval、Eval、Eval、Eval。你能看出代码哪里出错了吗？如果幸运的话，会有一些更直接明显的状态（如图 7.8 所示，调试器显示了 ex 参数的 ToString），但使用更有意义的方法名会有很大帮助。

就我个人而言，我喜欢将代码分解成简洁的方法，因此 switch 语句中块的使用会显著减少：

```csharp
static int Eval(Expression ex)
{
    switch (ex.NodeType)
    {
        case ExpressionType.Constant:
            return EvalConstant((ConstantExpression)ex);
        case ExpressionType.Add:
            return EvalBinary((BinaryExpression)ex, (a, b) => a + b);
        case ExpressionType.Multiply:
            return EvalBinary((BinaryExpression)ex, (a, b) => a * b);
        // Other binary operations.
        default:
            throw new NotSupportedException("Can't evaluate " + ex + ".");
    }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_400_0.png)

图 7.8 由于过度使用 switch 块而导致混淆的调用堆栈。

不过，我忍不住在 EvalBinary 中使用了一个小 lambda 表达式来简化二元运算符的 case。你将在第 17 章“委托”中看到更多关于 lambda 用法的内容，并在第 19 章“语言集成查询基础”和第 20 章“语言集成查询内部机制”中介绍 LINQ 时看到更多相关内容。

还要注意这里自信地使用了强制转换表达式，而不是万无一失的 as 关键字。在这种情况下，我们确信类型为 Add 的表达式必须是 BinaryExpression。如果你确信如此，就使用强制转换！

## 健壮的求值器

在前面的代码片段中编写求值器所采用的方法非常标准。它被称为“递归下降”，因为我们递归地下降表达式树。这种方法的一个潜在问题是其调用栈行为；非常复杂的表达式耗尽调用栈空间并导致 StackOverflowException 并非不可想象。存在替代方案，但超出了本书的范围。因此，如果你需要编写一个应对深度嵌套输入仍能保持弹性的递归求值器，一定要测试这个潜在问题。

在内部，switch 语句是在 IL 指令集的直接协助下实现的。为简单起见，我们仅使用基于 int 的 switch 进行说明：
