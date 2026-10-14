

通过显式请求容量，我们在添加新元素之前为 count 个项目分配足够的内存，这样列表在用完空间时就不需要调整大小了。如果我们重新运行性能测试，如表 8-25 所示，结果与之前的测试更为一致。

## 表 8-25：预分配列表的容量

| 方法 | 时间 (ms) | 签名 |
|---|---|---|
| 100% ToList | 426 | ToList(Int32) |
| 63.0% MakePurchase | 268 | MakePurchase(Int32) |
| 4.28% MoveNext | 18 | System.Linq.Enumerable+ RangeIterator .MoveNext() |
| 1.41% get_Current | 6.0 | System.Linq.Enumerable+ Iterator`1 .get_Current() |

我们的测试表明，使用 LINQ，至少对于生成元素序列这种相对简单的任务而言，其效率不低于使用 foreach 循环。我们还可以尝试另一种方法：for 循环。

## 循环方法

我们创建 Purchase 对象列表的方法基于创建一系列 int 值，并使用 Select 方法将其转换为新的 Purchase 对象序列。清单 8-27 展示了如何使用基本的 for 循环实现相同的结果，该循环不依赖迭代器，只是按照循环条件指定的次数运行循环体。

```
public static List<Purchase> ToList(int count)
{
    var items = new List<Purchase>(count);
    for(int i = 0; i != count; ++i)
    {
        items.Add(MakePurchase(i));
    }
    return items;
}
```

清单 8-27：使用简单的 for 循环

正如我们对 foreach 循环所做的那样，我们必须在进入循环之前创建目标 List<Purchase>，并使用构造函数设置其容量。在循环体中，我们使用 MakePurchase 方法添加新的 Purchase，如前所述。表 8-26 显示了使用 for 循环创建 1000 万个 Purchase 对象的分析器报告。

## 表 8-26：直接 for 循环性能

| 方法 | 时间 (ms) | 签名 |
|---|---|---|
| 100% ToList | 417 | ToList(Int32) |
| 67.3% MakePurchase | 281 | MakePurchase(Int32) |
| 5.70% op_Implicit | 24 | System.Decimal.op_Implicit(Int32) |

再次，for 循环方法与我们尝试过的其他方法之间没有显著的性能差异。使用 LINQ 与使用 foreach 或 for 循环之间的主要区别在于风格：LINQ 代码更直接，允许我们以声明方式表达意图，而 for 和 foreach 循环更具过程性。LINQ 表达式使我们能够专注于所需的结果，而两种循环方法则专注于要遵循的步骤或指令。

## 模式匹配与选择

声明式风格而非过程式风格的一个常见好处是，我们可以用更少的代码实现相同的结果。虽然这节省了我们输入的量，但这只是副作用。真正的益处在于减少了人类阅读者需要理解的语法。用 LINQ 风格的函数式表达式替换显式循环就是一个例子。许多 LINQ 表达式在内部基于循环，但循环结构本身对用户代码是隐藏的。使用循环和显式条件手动迭代序列容易出错，而且复杂的循环结构通常比调用 Select 或 ToList 等方法更难让人类阅读者理解。

声明式技术的另一个常见应用是在选择代码中：用模式匹配表达式替换 if 和 switch 语句。考虑清单 8-28 中的构造函数，它通过将参数值与某些模式指定的规则进行匹配来验证参数值。

```
private const double ZeroKelvin = -273.15;

private Temperature(double celsius)
    => amount = celsius switch
    {
        double.NaN
            => throw new ArgumentException(--snip--),

        < ZeroKelvin or double.PositiveInfinity
            => throw new ArgumentOutOfRangeException(--snip--),

        _ => celsius
    };
```

清单 8-28：用于验证的模式匹配

Temperature 构造函数如果给定的参数是 double.NaN 则抛出异常，并且还禁止小于 ZeroKelvin 或等于 PositiveInfinity 的值。不匹配这两个规则的 celsius 参数值会通过丢弃模式分配给 amount 字段，该模式是 switch 表达式中的最后一个模式。

将清单 8-28 与清单 8-29 进行比较，后者实现了完全相同的结果，但使用 if…else 语句测试传入的参数值。

```
private Temperature(double celsius)
{
    if(celsius is double.NaN)
    {
        throw new ArgumentException(--snip--);
    }
    else if(celsius < ZeroKelvin || celsius is double.PositiveInfinity)
    {
        throw new ArgumentOutOfRangeException(--snip--);
    }
    else
    {
        this.amount = celsius;
    }
}
```

清单 8-29：使用 if 和 else 链进行验证

我们可以通过删除冗余的 else 语句并允许 if 块在值不满足 if 条件时继续执行，从而使此代码的语法负担更小。虽然这样做会使代码更短，但如果添加新条件，则更容易出错。

另一种选择是使用 switch 语句，如清单 8-30 所示。

```
switch (celsius)
{
    case double.NaN:
        throw new ArgumentException(--snip--);

    case < ZeroKelvin:
    case double.PositiveInfinity:
        throw new ArgumentOutOfRangeException(--snip--);

    default:
        this.amount = celsius;
        break;
}
```

清单 8-30：使用 switch 语句进行验证

此版本更接近清单 8-28 中的 switch 表达式，并且两种形式的 switch 很容易混淆。主要区别在于，这里我们在 default 分支中分配 amount 字段，而在 switch 表达式中，amount 字段被赋值为整个表达式的值。

与本章其余部分不同，我们不需要运行性能分析来比较清单 8-28 至 8-30，因为编译器为每种情况生成的代码几乎相同——大致与清单 8-29 所示的代码相同。编译器可能会改变 CIL 中条件的顺序，但这不会以任何方式改变逻辑。

## 总结

> 我们不认为仅仅因为资源便宜就挥霍使用资源是一种良好的工程实践。
> —Niklaus Wirth，《Project Oberon: The Design of an Operating System, a Compiler, and a Computer》

手工优化的代码通常更难让人类阅读者理解，通常是因为它经常涉及用更低级的结构替换简单的惯用法，例如循环和模式匹配。当程序运行速度比我们认为的慢时，很容易直接深入并更改我们怀疑是瓶颈的代码部分。然而，程序员的优化直觉 notoriously 不可靠。我们可能会使代码更难阅读，同时在任何有意义的程度上都无法改善性能。

手工优化代码几乎总是以清晰度和简洁性换取性能。我们只能通过在更改前后测量性能来判断这是否是一笔合理的交易。即使我们在代码的某个部分提高了性能，我们仍必须决定是否使代码变得不那么清晰，如果是这样，改变是否合理。我们还必须确保我们的优化没有以任何方式改变程序的行为。缓慢但正确的代码总是优于性能再好也不正确的代码。这并不意味着足够好就不能正确——经常需要在性能与准确性或精度之间做出妥协——但我们需要知道不准确在何时真正意味着不正确。

使用众所周知的惯用语和模式有助于人类阅读者轻松理解代码。相应地，当我们偏离这些常见设计时，我们使代码更难遵循。因此，我们必须有选择地将优化应用于能带来最大收益的代码区域。

重写 Equals 的行为对于绝大多数类型来说并不困难，但它增加了任何需要理解我们代码的人的额外认知负担的实现细节。

使用记录来表示值类型可以消除其中大部分额外复杂性，因为编译器会为我们生成正确的实现。然而，即使接受默认行为也不一定能产生最有效的代码。

由分析器证据支持的谨慎代码优化可以在速度和内存使用方面带来更好的性能。现代计算机速度很快，通常拥有足够的内存，但这并不意味着我们应该浪费任何资源。
