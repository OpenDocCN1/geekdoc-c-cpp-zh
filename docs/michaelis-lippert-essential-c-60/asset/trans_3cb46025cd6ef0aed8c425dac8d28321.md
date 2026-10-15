

## 异或运算符 (^)

插入符号 ^ 是“异或”（XOR）运算符。当应用于两个布尔操作数时，XOR 运算符仅在恰好一个操作数为 true 时返回 true，如表 3.3 所示。

**表 3.3：XOR 运算符的条件值**

| 左操作数 | 右操作数 | 结果 |
|---|---|---|
| True | True | False |
| True | False | True |
| False | True | True |
| False | False | False |

与布尔 AND 和布尔 OR 运算符不同，布尔 XOR 运算符不会短路：它总是检查两个操作数，因为除非知道两个操作数的值，否则无法确定结果。请注意，XOR 运算符与布尔不等运算符完全相同。

## 逻辑否定运算符 (!)

逻辑否定运算符，或 NOT 运算符，!，会反转一个 bool 值。此运算符是一元运算符，意味着它只需要一个操作数。列表 3.34 演示了它的工作原理，输出 3.16 显示了结果。

**列表 3.34：使用逻辑否定运算符**

```csharp
bool valid = false;
bool result = !valid;
// Displays "result = True".
System.Console.WriteLine($"result = { result }");
```

**输出 3.16**

```text
result = True
```

在列表 3.34 的开头，valid 被设置为 false。然后你对 valid 使用否定运算符并将值赋给 result。

## 条件运算符 (?:)

为了代替用于选择两个值之一的 if-else 语句，你可以使用条件运算符。条件运算符同时使用问号和冒号；其通用格式如下：

```
condition ? consequence : alternative
```

条件运算符是“三元”运算符，因为它有三个操作数：condition、consequence 和 alternative。（由于它是 C# 中唯一的 ternary 运算符，它通常被称为“ternary 运算符”，但用其名称而不是操作数的数量来称呼它更清晰。）与逻辑运算符一样，条件运算符使用一种形式的短路。如果条件求值为 true，条件运算符仅求值 consequence。如果条件求值为 false，它仅求值 alternative。运算符的结果是求值后的表达式。

列表 3.35 说明了条件运算符的使用。该程序的完整列表出现在附录 B。

**列表 3.35：条件运算符**

```
class TicTacToe
{
    static string Main()
    {
        // Initially set the currentPlayer to Player 1
        int currentPlayer = 1;

        // ...

        for (int turn = 1; turn <= 10; turn++)
        {
            // ...

            // Switch players
            currentPlayer = (currentPlayer == 2) ? 1 : 2;
        }
    }
}
```

该程序交换当前玩家。为此，它检查当前值是否为 2。这是条件表达式的“条件”部分。如果条件的结果为 true，条件运算符的结果为“consequence”值 1。否则，它的结果为“alternative”值 2。与 if 语句不同，条件运算符的结果必须被赋值（或作为参数传递）；它不能单独作为整个语句出现。

## 指南

考虑使用 if/else 语句而不是过于复杂的条件表达式。

C# 语言要求条件运算符中的 consequence 和 alternative 表达式类型一致，并且该一致类型必须在不检查表达式周围上下文的情况下确定。例如，f ? "abc" : 123 不是合法的条件表达式，因为 consequence 和 alternative 分别是字符串和数字，两者都无法相互转换。即使你写 object result = f ? "abc" : 123; C# 编译器也会将此表达式标记为非法，因为与两个表达式一致的类型（即 object）在条件表达式之外找到。

## 空合并运算符 (??)

空合并运算符是表达“如果此值为 null，则使用此其它值”的简洁方式。它具有以下形式：

```
expression1 ?? expression2
```

空合并运算符也使用一种形式的短路。如果 expression1 不为 null，其值就是操作的结果，并且另一个表达式不会被求值。如果 expression1 求值为 null，则 expression2 的值是运算符的结果。与条件运算符不同，空合并运算符是二元运算符。

列表 3.36 说明了空合并运算符的使用。

**列表 3.36：空合并运算符**

```
string fileName = GetFileName();
// ...
string fullName = fileName ?? "default.txt";
// ...
```

在此列表中，我们使用空合并运算符将 fullName 设置为 "default.txt"，如果 fileName 为 null。如果 fileName 不为 null，fullName 只是被赋予 fileName 的值。

空合并运算符可以“链式”使用。例如，形式为 x ?? y ?? z 的表达式如果 x 不为 null 则结果为 x；否则如果 y 不为 null 则结果为 y；否则结果为 z。也就是说，它从左到右选择第一个非 null 表达式，或者如果所有前面的表达式都为 null，则使用最后一个表达式。

空合并运算符在 C# 2.0 版本中与可空值类型一起添加。此运算符适用于可空值类型和引用类型的两个操作数。

## 空条件运算符 (?.)

每当你在 null 值上调用方法时，运行时会抛出 System.NullReferenceException，这几乎总是表明编程逻辑存在错误。鉴于此模式的频繁出现（即在调用成员之前检查 null），C# 6.0 引入了 "?." 运算符，即空条件运算符：

**列表 3.37：空条件运算符**

```
class Program
{
    static void Main(string[] args)
    {
        if (args?.Length == 0)
        {
            System.Console.WriteLine(
                "ERROR: File missing. "
                + "Use:\\tfind.exe file:<filename>");
        }
        else
        {
            if (args[0]?.ToLower().StartsWith("file:")??false)
            {
                string fileName = args[0]?.Remove(0, 5);
                // ...
            }
        }
    }
}
```

空条件运算符在调用方法或属性（列表 3.37 中的第一个示例中的 Length）之前检查操作数（第一个 args）是否为空。逻辑上等效的显式代码如下（尽管在 C# 6.0 语法中 args 的值仅被求值一次）：

```
(args != null) ? (int?)args.Length : null
```

使空条件运算符特别方便的是它可以被链式使用。例如，如果你调用 args[0]?.ToLower() .StartsWith("file:")，只有当 args[0] 不为 null 时，ToLower() 和 StartsWith() 才会<|message|>被调用。当表达式被链式使用时，如果第一个操作数为 null，则表达式求值会被短路，并且在表达式调用链中不会发生进一步的调用。

然而，要小心不要无意中忽略额外的空条件运算符。例如，考虑如果（假设在此情况下）args[0]?.ToLower() 也可能返回 null 会发生什么。在这种情况下，在调用 StartsWith() 时会发生 NullReferenceException。这并不意味着你必须使用一系列空条件运算符，而是说你应该有意地设计逻辑。在此示例中，由于 ToLower() 永不为 null，因此不需要额外的空条件运算符。

关于空条件运算符需要注意的重要一点是，当与返回值类型成员一起使用时，它始终返回该类型的可空版本。例如，args?.Length 返回 int?，而不是简单的 int。类似地，args[0]?.ToLower().StartsWith("file:") 返回 bool?（一个 Nullable<bool>）。此外，由于 if 语句需要 bool 数据类型，因此有必要在 StartsWith() 表达式后跟随空合并运算符（??）。

尽管可能有点奇怪（与其它运算符行为相比），可空值类型的返回仅在调用链的末尾产生。因此，在 Length 上调用点（"."）运算符只允许调用 int（而不是 int?）成员。然而，将 args?.Length 括在括号中——从而通过括号运算符优先级强制 int? 结果——会调用 int? 返回值并使 Nullable<T> 特定成员（HasValue 和 Value）可用。

空条件运算符也可以与索引运算符结合使用，如列表 3.38 所示。

