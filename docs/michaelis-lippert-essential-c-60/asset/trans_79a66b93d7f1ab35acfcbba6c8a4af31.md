

## OUTPUT 3.18

```
and = 4
or = 15
xor = 11
```

在清单 3.40 中，值 7 是掩码；它用于使用特定的运算符表达式在第一个操作数中暴露或消除特定的位。请注意，与 AND (&&) 运算符不同，& 运算符总是评估两侧，即使左侧部分为 false。同样，OR 运算符的 | 版本也不是“短路”的。它总是评估两个操作数，即使左操作数为 true。因此，AND 和 OR 运算符的位版本不是短路的。

要将数字转换为其二进制表示，需要遍历数字中的每一位。清单 3.41 是一个将整数转换为其二进制表示的字符串的程序示例。清单 3.41 的结果出现在输出 3.19 中。

## LISTING 3.41: Getting a String Representation of a Binary Display

```
class BinaryConverter
{
    static void Main()
    {
        const int size = 64;
        ulong value;
        char bit;

        System.Console.Write ("Enter an integer: ");
        // Use Long.Parse() to support negative numbers
        // Assumes unchecked assignment to ulong.
        value = (ulong)long.Parse(System.Console.ReadLine());

        // Set initial mask to 100...
        ulong mask = 1UL << size - 1;
        for (int count = 0; count < size; count++)
        {
            bit = ((mask & value) != 0) ? '1' : '0';
            System.Console.Write(bit);
            // Shift mask one location over to the right
            mask >>= 1;
        }
        System.Console.WriteLine();
    }
}
```

![](img/25683ccec0773ba5b8794b11f2b12877_171_0.png)

在清单 3.41 的 for 循环的每次迭代中（将在本章后面讨论），我们使用右移赋值运算符为 value 中的每个位位置创建一个掩码。通过使用 & 位运算符屏蔽特定位，我们可以确定该位是否被设置。如果掩码测试产生非零结果，我们向控制台写入 1；否则，我们写入 0。以这种方式，23 创建描述无符号长整型二进制值的输出。

还请注意，(mask & value) != 0 中的括号是必要的，因为不等式的优先级高于 AND 运算符。如果没有显式的括号，此表达式将等同于 mask & (value != 0)，这没有任何意义；& 的左侧是 ulong，右侧是 bool。

这个特定示例仅用于学习目的。实际上有一个内置的 CLR 方法，System.Convert.ToString(value, 2) 可以执行此类转换。事实上，第二个参数指定基数（例如，二进制为 2，十进制为 10，十六进制为 16），允许不仅仅是转换为二进制。

## Bitwise Compound Assignment Operators (&=, |=, ^=)

不出所料，您可以将这些按位运算符与赋值运算符组合如下：&=、|= 和 ^=. 因此，您可以取一个变量，用数字进行 OR 操作，并将结果赋回原始变量，清单 3.42 演示了这一点。

```
byte and = 12, or = 12, xor = 12;
and &= 7;    // and = 4
or |= 7;     // or = 15
xor ^= 7;    // xor = 11
System.Console.WriteLine(
    $"and = { and } \nor = { or } \nxor = { xor }");
```

清单 3.42 的结果出现在输出 3.20 中。

```
and = 4
or = 15
xor = 11
```

使用类似 fields & mask 将位图与掩码组合，清除在掩码中未设置的 fields 中的位。相反，fields &= ~mask 清除在掩码中设置的 fields 中的位。

## Bitwise Complement Operator (~)

**按位补码运算符** 取操作数中每个位的补码，其中操作数可以是 int、uint、long 或 ulong。因此，表达式 ~1 返回二进制表示为 1111 1111 1111 1111 1111 1111 1111 1110 的值，而 ~(1<<31) 返回二进制表示为 0111 1111 1111 1111 1111 1111 1111 1111 的数字。

## Control Flow Statements, Continued

现在我们已经更详细地描述了布尔表达式，我们可以更清晰地描述 C# 支持的控制流语句。其中许多语句对经验丰富的程序员来说都很熟悉，因此您可以浏览本节查找 C# 特定的细节。特别注意 foreach 循环，因为这对许多程序员来说可能是新的。

## The while and do/while Loops

到目前为止，您已经学习了如何编写仅执行一次的程序。然而，计算机可以轻松地多次执行类似的操作。为此，您需要创建一个指令循环。我们将讨论的第一个指令循环是 while 循环，因为它是最简单的条件循环。while 语句的一般形式如下：

```
while (condition)
    statement
```

只要条件（必须是布尔表达式）计算为 true，计算机就会重复执行循环的“主体”语句。如果条件计算为 false，代码执行将跳过主体并执行循环语句之后的语句。请注意，即使 statement 导致条件变为 false，statement 也会继续执行。循环仅在“循环顶部”重新评估条件时退出。清单 3.43 中显示的 Fibonacci 计算器演示了 while 循环。

## LISTING 3.43: while Loop Example

```
class FibonacciCalculator
{
    static void Main()
    {
        decimal current;
        decimal previous;
        decimal temp;
        decimal input;

        System.Console.Write("Enter a positive integer:");

        // decimal.Parse convert the ReadLine to a decimal.
        input = decimal.Parse(System.Console.ReadLine());

        // Initialize current and previous to 1, the first
        // two numbers in the Fibonacci series.
        current = previous = 1;

        // While the current Fibonacci number in the series is
        // Less than the value input by the user.
        while (current <= input)
        {
            temp = current;
            current = previous + current;
            previous = temp; // Executes even if previous
            // statement caused current to exceed input
        }

        System.Console.WriteLine(
            $"The Fibonacci number following this is { current }");
    }
}
```

Fibonacci 数是 Fibonacci 数列的成员，该数列包括所有数字，这些数字是数列中前两个数字之和，从 1 和 1 开始。在清单 3.43 中，您提示用户输入一个整数。然后您使用 while 循环找到第一个大于用户输入的数字的 Fibonacci 数。

## BEGINNER TOPIC

## When to Use a while Loop

本章的其余部分考虑了导致代码块重复执行的其他语句。术语循环体指的是要在 while 语句中执行的语句（通常是代码块），因为代码在“循环”中执行，直到达到退出条件为止。了解选择哪种循环结构非常重要。您使用 while 结构在条件计算为 true 时进行迭代。每当重复次数已知时，例如从 0 计数到 n 时，最适合使用 for 循环。do/while 与 while 循环类似，只是它保证至少执行一次循环体。

do/while 循环与 while 循环非常相似，只是当重复次数从 1 到 n 且在迭代开始时 n 未知时，首选 do/while 循环。这种模式经常出现在提示用户输入时。清单 3.44 取自井字游戏程序。

## LISTING 3.44: do/while Loop Example

```
// Repeatedly request player to move until he
// enters a valid position on the board.
bool valid;
do
{
    valid = false;

    // Request a move from the current player.
    System.Console.Write(
        $"\nPlayer {currentPlayer}: Enter move:");
    input = System.Console.ReadLine();

    // Check the current player's input.
    // ...
} while (!valid);
```

在清单 3.44 中，您在每次迭代或循环重复开始时将 valid 初始化为 false。接下来，您提示并检索用户输入的数字。虽然此处未显示，但您随后检查输入是否正确，如果正确，则将 valid 赋值为 true。由于代码使用 do/while 语句而不是 while 语句，用户将被提示至少输入一次。

do/while 循环的一般形式如下：

