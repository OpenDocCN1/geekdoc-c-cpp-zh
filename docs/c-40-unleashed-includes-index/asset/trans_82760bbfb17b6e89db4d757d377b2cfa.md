
- TryExpression 是通过表达式树 API 构造异常处理代码的一站式方案。除了主体表达式外，它还接受一个可选的 fault 和 finally 处理块，以及一个可选的处理器列表（以 CatchBlock 对象表示，包含处理器代码、要捕获的异常类型和一个可选过滤器）。

## 那么类型呢？

等一下……Expression 基类型不是有一个 Type 属性吗？你不是说过表达式有值而语句没有吗？那么，语句树节点上的类型是怎么回事？

如果你只站在 C# 的立场上思考，你的这个看法完全正确。然而，相当多的语言（尤其是动态语言和函数式语言）会将更多的语言构造视为有值的表达式，包括代码块。例如，在 Ruby 中，块中最后一条被执行的语句（考虑到这条旁注，或许我们该称之为表达式）将作为整个块的结果值。对于 if 语句，这基本上就像我们在 C# 中熟知的条件三元运算符。对于 for 循环，循环体在最后一次迭代中的值将提供循环的有值结果。

由于表达式树构成了 DLR 基础设施的重要组成部分，因此遵循这一设计并不令人意外。然而，这一选择并不妨碍你在表达式树中捕获 C# 中无值块的语义。诀窍是将块类型设为 System.Void，仅此而已。这是一个考虑通用用途的巧妙设计，不是吗？

除了引入新的树节点类型外，ExpressionType 枚举还新增了一大批值。其中一些值用于新的 Expression 子类型，而另一些则用于与现有标准树节点（如 BinaryExpression）配合使用。大多数新的枚举值都与各种赋值相关，例如 Assign（用于 a = b 的形式）、各种复合赋值（如用于 a += b 形式的 AddAssign），以及递增或递减操作（如用于广为人知且备受喜爱的 i++ 形式的 PostIncrementAssign）。

例如，下面这段代码将利用各种新的表达式树特性，通过运行时生成的代码打印数字 0 到 9。其中的内联注释展示了对应的 C# 代码：

```csharp
var i = Expression.Variable(typeof(int), "i");
var brk = Expression.Label("Break");
var a = Expression.Lambda<Action>(
    Expression.Block(
        new[] { i },
        // int i = 0;
        Expression.Assign(i, Expression.Constant(0)),
        // while (true)
        Expression.Loop(
            // {
            Expression.Block(
                // if
                Expression.IfThen(
                    // (i == 10)
                    Expression.Equal(i, Expression.Constant(10)),
                    // break;
                    Expression.Goto(brk)
                ),
                // Console.WriteLine(i);
                Expression.Call(
                    typeof(Console).GetMethod("WriteLine", new[] { typeof(int) }),
                    i
                ),
                // i++;
                Expression.PostIncrementAssign(i)
            ),
            brk
            // }
        )
    )
);
var f = a.Compile();
f(); // Prints 0 to 9
```

尽管如果你需要在运行时动态生成代码，这一切都很漂亮，但你可能会担心调试支持的问题。对此有两个答案。首先，工厂方法会对它们能发现的所有语义错误抛出异常，确保你的树结构良好。其次，.NET 4 和 Visual Studio 2010 中新增了一个调试器可视化工具，帮助你以更易理解的形式检查表达式树的外观。如果你有一段代码将多个部分拼接成更大的树，这尤其有用。图 21.22 显示了当鼠标悬停在表达式树对象上时，打开可视化工具的图标出现的位置。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1132_0.png)

图 21.23 展示了该工具提供的可视化效果，以文本块的形式表示表达式树。从中你可以看到许多信息。首先，所有节点显然都有类型；甚至 If 的 else 分支（我们从未显式声明过）也有

## 使用 ExpressionVisitor

正如在第 20 章讨论 LINQ 提供程序时提到的，在必须在运行时解释用户意图的场景中，表达式树特别有用；例如，转换查询表达式。为了实现这一点，编译器为 lambda 表达式实现了同像性（homoiconicity）特性，这样用户就不必手动编写表达式树。

在表达式树运行时解释的整个图景中，另一个利益相关者是希望在运行时对这样的表达式树执行分析的库或应用程序开发人员。由于表达式树具有深度递归的特性，这似乎是一项艰巨的任务。但幸运的是，这是一项可以相当容易地提供标准工具的任务。开发人员分析表达式树的主要工具是 .NET 中引入的 ExpressionVisitor 类型。

访问者是一种众所周知的设计模式，用于实现对某种数据结构中节点进行访问的“策略”。对于 ExpressionVisitor，它会执行对表达式树的深度优先遍历。在访问节点时，会调用一个方法，将正在访问的节点暴露给知道如何处理当前任务的用户代码。例如，在 LINQ 提供程序的转换过程中使用访问者，将实现将所有节点转换为目标查询语言（如 SQL）的转换。

前面你已经在 Expression 基类型上看到了对访问者的内置支持的踪迹，即几个方法：VisitChildren 和 Accept。关于这些方法的背景信息，请参阅 MSDN 文档。

要创建表达式树访问者，需要从 ExpressionVisitor 基类派生一个类，并重写访问者想要处理的任何专用访问方法。这里展示了一个简单的访问者示例，重写了 VisitBinary 来处理树中加法操作的使用：

```csharp
class FindAdditions : ExpressionVisitor
{
    protected override Expression VisitBinary(BinaryExpression node)
    {
        if (node.NodeType == ExpressionType.Add)
            Console.WriteLine(node.Left + " added to " + node.Right);
        return base.VisitBinary(node);
    }
}
```

注意对基类调用的使用，它将递归执行到子树的左右两侧。下面这段代码运行 FindAdditions 访问者：

```csharp
Expression<Func<int, int, int, int>> sum = (x, y, z) => x + y + z + 1;
var fa = new FindAdditions();
fa.Visit(sum);
```

屏幕上会打印三条消息。这留作练习，由你来推断这些消息是什么。（提示：回想一下加法运算符的结合律性质。）

由于访问者的 Visit 方法返回一个 Expression，它们可用于将树转换为新树（例如，执行优化）。访问者基类的默认实现仅返回与原始节点等价的节点，同时仍会访问其中的所有节点。一个更直接有用的例子是布尔逻辑优化器，它试图在保持语义的同时降低布尔表达式的复杂度：

```csharp
class BooleanLogicOptimizer : ExpressionVisitor
{
    protected override Expression VisitUnary(UnaryExpression node)
    {
        // If we represent a ! operator...
        if (node.NodeType == ExpressionType.Not)
        {
            // ...and the recursive visit to our operand...
            var res = base.Visit(node.Operand);
            // ...is also a ! operator...
            if (res.NodeType == ExpressionType.Not)
            {
                // ...then we can forget about the double negation:
                return ((UnaryExpression)res).Operand;
            }
        }
        return base.VisitUnary(node);
    }
}
```

在这个示例中，我们只实现了针对双重否定的优化器，但我们可以同样轻松地扩展它，加入适用于布尔逻辑的更复杂规则（如德摩根定律，或仅由 AND 和 NOT 组成的某种范式的方法）。对于下面这个例子，四个多余的否定将被削减掉：

```csharp
Expression<Func<bool, bool>> b1 = x => !!!!x;
Console.WriteLine(b1);
var b1o = new BooleanLogicOptimizer();
Console.WriteLine(b1o.Visit(b1));
```

这里我们依赖表达式树的 ToString 行为，以可读的形式将它们打印到屏幕上，如图 21.24 所示。
