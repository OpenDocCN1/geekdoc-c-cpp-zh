
```
uint bal = 350;
Currency balance = bal;
uint bal2 = (uint)balance;
```

答案不是 350 而是 3！而且这一切都是合乎逻辑的。你将 350 隐式转换为 Currency，结果为 balance.Dollars = 3，balance.Cents = 50。然后编译器会像往常一样计算回转转换的最佳路径。Balance 最终会被隐式转换为 float（值为 3.5），然后显式转换为值为 3 的 uint。

当然，也存在其他情况，将数据转换为另一种数据类型再转换回来会导致数据丢失。例如，将包含 5.8 的 float 转换为 int 再转换回 float 会丢失小数部分，结果为 5，但从原则上讲，丢失数字的小数部分与将整数除以 100 以上是有细微差别的。Currency 突然变成了一个相当危险的类，对整数做了奇怪的事情！

问题在于你的转换对整数的解释存在冲突。Currency 与 float 之间的转换将整数值 1 解释为对应一美元，但最新的 uint 到 Currency 转换却将该值解释为一美分。这是一个非常糟糕设计的例子。如果你希望你的类易于使用，就应该确保所有转换的行为相互兼容，即它们直观上给出相同的结果。在这种情况下，解决方案显然是重写 uint 到 Currency 的转换，使其将整数值 1 解释为一美元：

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}
```

顺便说一下，你可能会想知道这个新的转换是否完全必要。答案是它可能有用。没有这个转换，编译器执行 uint 到 Currency 转换的唯一方式就是通过 float。直接转换在这方面效率更高，因此拥有这个额外的转换可以带来性能优势，不过你需要确保它给出与通过 float 相同的结果，而你现在已经做到了。在其他情况下，你可能会发现为不同的预定义数据类型分别定义转换可以使更多转换变为隐式而不是显式，不过这里并非如此。

判断你的转换是否兼容的一个好方法是问：无论转换走哪条路径，是否会给出相同的结果（除了像 float 到 int 转换那样可能损失精度之外）。Currency 类对此提供了一个很好的例子。看这段代码：

```
Currency balance = new Currency(50, 35);
ulong bal = (ulong) balance;
```

目前，编译器实现此转换只有一种方式：先隐式将 Currency 转换为 float，然后显式转换为 ulong。float 到 ulong 的转换需要显式转换，但这没问题，因为你在这里指定了显式转换。

然而，假设你随后添加了另一个转换，隐式地将 Currency 转换为 uint。你实际上会通过修改 Currency 结构体并添加到 uint 和从 uint 的转换来实现这一点。此代码作为 SimpleCurrency2 示例提供：

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}

public static implicit operator uint (Currency value)
{
    return value.Dollars;
}
```

现在编译器有了另一种可能的路径将 Currency 转换为 ulong：先隐式将 Currency 转换为 uint，然后隐式转换为 ulong。它会选择哪一条路径？如果存在多种可能性，C# 对编译器的最佳路径有一些精确的规则。（本书中未详细介绍这些规则，但如果你感兴趣，详细信息可在 MSDN 文档中找到。）最好的答案是，你应该设计你的转换，使所有路径给出相同的答案（除了可能的精度损失），在这种情况下，编译器选择哪一个其实并不重要。（碰巧的是，在本例中，编译器更倾向于选择 Currency 到 uint 再到 ulong 的路径，而不是 Currency 到 float 再到 ulong。）

要测试 SimpleCurrency2 示例，请将此代码添加到 SimpleCurrency 的测试代码中：

```
try
{
    Currency balance = new Currency(50,35);
    Console.WriteLine(balance);
    Console.WriteLine("balance is " + balance);
    Console.WriteLine("balance is (using ToString()) " + balance.ToString());
    uint balance3 = (uint) balance;
    Console.WriteLine("Converting to uint gives " + balance3);
}
```

代码片段 SimpleCurrency2/Program.cs

现在运行该示例会得到以下结果：

## SIMPLECURRENCY2

```
50
balance is $50.35
balance is (using ToString()) $50.35
Converting to uint gives 50
After converting to float, = 50.35
After converting back to Currency, = $50.34
Now attempt to convert out of range value of -$50.50 to a Currency:
Result is $4294967246.00
```

输出显示转换到 uint 已成功，尽管在进行此转换时你已丢失 Currency 的美分部分。将负 float 转换为 Currency 也产生了预期的溢出异常，因为 float 到 Currency 的转换本身现在定义了 checked 上下文。

然而，输出也演示了在使用转换时你需要了解的最后一个潜在问题。输出的第一行并未正确显示 balance，显示的是 50 而不是 $50.35。考虑以下这些行：

```
Console.WriteLine(balance);
Console.WriteLine("balance is " + balance);
Console.WriteLine("balance is (using ToString()) " + balance.ToString());
```

只有最后两行才正确地将 Currency 显示为字符串。发生了什么？这里的问题是，当你将转换与方法重载结合使用时，会产生另一个不可预测的来源。我们将按相反顺序查看这些行。

第三个 Console.WriteLine() 语句显式调用 Currency.ToString() 方法，确保 Currency 以字符串形式显示。第二个没有这样做。然而，传递给 Console.WriteLine() 的字符串字面量 "balance is" 使编译器清楚地知道参数应被解释为字符串。因此，Currency.ToString() 方法将被隐式调用。

然而，第一个 Console.WriteLine() 方法只是简单地将原始 Currency 结构体传递给 Console.WriteLine()。现在，Console.WriteLine() 有许多重载，但其中没有一个接受 Currency 结构体。因此，编译器会开始尝试寻找可以将 Currency 转换为什么类型以匹配 Console.WriteLine() 的某个重载。碰巧的是，Console.WriteLine() 的其中一个重载设计用于快速高效地显示 uint，并接受 uint 作为参数——你现在提供了一个将 Currency 隐式转换为 uint 的转换。

你像这样调用这些方法：

```csharp
using System;

namespace Wrox.ProCSharp.Delegates
{
    delegate double DoubleOp(double x);

    class Program
    {
        static void Main()
        {
            DoubleOp[] operations =
            {
                MathOperations.MultiplyByTwo,
                MathOperations.Square
            };

            for (int i=0; i < operations.Length; i++)
            {
                Console.WriteLine("Using operations[{0}]: ", i);
                ProcessAndDisplayNumber(operations[i], 2.0);
                ProcessAndDisplayNumber(operations[i], 7.94);
                ProcessAndDisplayNumber(operations[i], 1.414);
                Console.WriteLine();
            }

            static void ProcessAndDisplayNumber(DoubleOp action, double value)
            {
                double result = action(value);
                Console.WriteLine(
                    "Value is {0}, result of operation is {1}", value, result);
            }
        }
    }
}
```

代码片段 SimpleDelegate/Program.cs

在这段代码中，你实例化了一个 DoubleOp 委托数组（记住，在定义委托类后，你基本上可以像普通类一样实例化实例，因此将它们放入数组中没有问题）。数组的每个元素都被初始化为引用 MathOperations 类实现的不同操作。然后，你遍历数组，将每个操作应用于三个不同的值。这说明了使用委托的一种方式——你可以使用它们将方法组合到数组中，以便在循环中调用多个不同的方法。

此代码中的关键行是实际将每个委托传递给 ProcessAndDisplayNumber() 方法的行，例如：

```
ProcessAndDisplayNumber(operations[i], 2.0);
```

在这里，你传递的是委托的名称但没有参数。鉴于 operations[i] 是一个委托，从语法上讲：
- operations[i] 表示委托（即委托所代表的方法）。
- operations[i] (2.0) 表示实际调用此方法，将括号中的值作为参数传入。
