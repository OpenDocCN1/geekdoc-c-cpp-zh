
```csharp
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

在清单 3.41 的`for`循环的每次迭代中（将在本章后面讨论），我们使用右移赋值运算符为`value`中的每个位位置创建一个掩码。通过使用`&`位运算符屏蔽特定位，我们可以确定该位是否被设置。如果掩码测试产生非零结果，我们向控制台写入 1；否则，我们写入 0。以这种方式，23 创建描述无符号长整型二进制值的输出。

还请注意，`(mask & value) != 0`中的括号是必要的，因为不等式的优先级高于 AND 运算符。如果没有显式的括号，此表达式将等同于`mask & (value != 0)`，这没有任何意义；`&`的左侧是`ulong`，右侧是`bool`。

这个特定示例仅用于学习目的。实际上有一个内置的 CLR 方法，`System.Convert.ToString(value, 2)`可以执行此类转换。事实上，第二个参数指定基数（例如，二进制为 2，十进制为 10，十六进制为 16），允许不仅仅是转换为二进制。

## Bitwise Compound Assignment Operators (&=, |=, ^=)

不出所料，您可以将这些按位运算符与赋值运算符组合如下：`&=`、`|=`和`^=`。因此，您可以取一个变量，用数字进行 OR 操作，并将结果赋回原始变量，清单 3.42 演示了这一点。

```csharp
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

使用类似`fields & mask`将位图与掩码组合，清除在掩码中未设置的`fields`中的位。相反，`fields &= ~mask`清除在掩码中设置的`fields`中的位。

## Bitwise Complement Operator (~)

**按位补码运算符** 取操作数中每个位的补码，其中操作数可以是`int`、`uint`、`long`或`ulong`。因此，表达式`~1`返回二进制表示为 1111 1111 1111 1111 1111 1111 1111 1110 的值，而`~(1<<31)`返回二进制表示为 0111 1111 1111 1111 1111 1111 1111 1111 的数字。

## Control Flow Statements, Continued

现在我们已经更详细地描述了布尔表达式，我们可以更清晰地描述 C# 支持的控制流语句。其中许多语句对经验丰富的程序员来说都很熟悉，因此您可以浏览本节查找 C# 特定的细节。特别注意 `foreach` 循环，因为这对许多程序员来说可能是新的。

### The while and do/while Loops

到目前为止，您已经学习了如何编写仅执行一次的程序。然而，计算机可以轻松地多次执行类似的操作。为此，您需要创建一个指令循环。我们将讨论的第一个指令循环是`while`循环，因为它是最简单的条件循环。`while`语句的一般形式如下：

```
while (condition)
    statement
```

只要条件（必须是布尔表达式）计算为`true`，计算机就会重复执行循环的“主体”语句。如果条件计算为`false`，代码执行将跳过主体并执行循环语句之后的语句。请注意，即使`statement`导致条件变为`false`，`statement`也会继续执行。循环仅在“循环顶部”重新评估条件时退出。清单 3.43 中显示的 Fibonacci 计算器演示了`while`循环。

#### LISTING 3.43: while Loop Example

```csharp
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

Fibonacci 数是 Fibonacci 数列的成员，该数列包括所有数字，这些数字是数列中前两个数字之和，从 1 和 1 开始。在清单 3.43 中，您提示用户输入一个整数。然后您使用`while`循环找到第一个大于用户输入的数字的 Fibonacci 数。

#### BEGINNER TOPIC: When to Use a while Loop

本章的其余部分考虑了导致代码块重复执行的其他语句。术语循环体指的是要在`while`语句中执行的语句（通常是代码块），因为代码在“循环”中执行，直到达到退出条件为止。了解选择哪种循环结构非常重要。您使用`while`结构在条件计算为`true`时进行迭代。每当重复次数已知时，例如从 0 计数到 n 时，最适合使用`for`循环。`do/while`与`while`循环类似，只是它保证至少执行一次循环体。

`do/while`循环与`while`循环非常相似，只是当重复次数从 1 到 n 且在迭代开始时 n 未知时，首选`do/while`循环。这种模式经常出现在提示用户输入时。清单 3.44 取自井字游戏程序。

##### LISTING 3.44: do/while Loop Example

```csharp
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

在清单 3.44 中，您在每次迭代或循环重复开始时将`valid`初始化为`false`。接下来，您提示并检索用户输入的数字。虽然此处未显示，但您随后检查输入是否正确，如果正确，则将`valid`赋值为`true`。由于代码使用`do/while`语句而不是`while`语句，用户将被提示至少输入一次。

`do/while`循环的一般形式如下：

```
do
    statement
while (condition);
```

与所有控制流语句一样，通常使用代码块作为单个语句，以便将多个语句作为循环体执行。然而，除了带标签的语句或局部变量声明之外的任何单个语句都可以使用。

### The for Loop

`for`循环在达到指定条件之前反复执行代码块。这样，它与`while`循环非常相似。不同之处在于，`for`循环具有内置的语法用于初始化、递增和测试计数器的值，该计数器称为 **loop variable**。由于循环语法中有一个专门的位置用于递增操作，因此递增和递减运算符经常作为`for`循环的一部分使用。

Listing 3.45 显示了使用`for`循环以二进制形式显示整数（功能等同于调用 BCL 静态函数`System.Convert.ToString()`且`toBase`值为 2）。该列表的结果出现在 Output 3.21 中。

#### LISTING 3.45: Using the for Loop

```csharp
class BinaryConverter
{
    static void Main()
    {
        const int size = 64;
        ulong value;
        char bit;

        System.Console.Write("Enter an integer: ");

        // Use long.Parse() so as to support negative numbers.
        // Assumes unchecked assignment to ulong.
        value = (ulong)long.Parse(System.Console.ReadLine());

        // Set initial mask to 100....
        ulong mask = 1UL << size - 1;

        for (int count = 0; count < size; count++)
        {
            bit = ((mask & value) > 0) ? '1' : '0';
            System.Console.Write(bit);

            // Shift mask one location over to the right
            mask >>= 1;
        }
    }
}
```

#### OUTPUT 3.21

```
Enter an integer: -42
1111111111111111111111111111111111111111111111111010110
```

Listing 3.45 对位掩码执行 64 次操作，每次对应数字中的一位。`for`循环头部的三个部分首先声明并初始化变量`count`，然后描述循环体必须满足的条件，最后描述更新循环变量的操作。`for`循环的一般形式如下：

```
for (initial ; condition ; loop)
    statement
```

以下是`for`循环的分解。

- `initial`部分执行在第一次迭代之前的操作。在 Listing 3.45 中，它声明并初始化变量`count`。初始表达式不必是新变量的声明（尽管经常是）。例如，可以在之前声明变量，然后仅在`for`循环中初始化它，或者通过将其留空来完全跳过初始化部分。在此处声明的变量在`for`语句的头部和主体范围内。

- `for`循环的条件部分指定结束条件。当此条件为假时，循环退出，就像`while`循环一样。`for`循环只要条件计算结果为真，就会执行主体。在前面的示例中，当`count`大于或等于 64 时，循环退出。

- 循环表达式在每次迭代后执行。在前面的示例中，`count++`在掩码的右移（`mask >>= 1`）之后执行，但在条件被评估之前。在第六十四次迭代期间，`count`增加到 64，导致条件变为假，从而终止循环。

- `for`循环的`statement`部分是“循环体”代码，只要条件表达式保持为真，就会执行该代码。

如果不使用`for`循环表达式，以伪代码形式写出每个`for`循环执行步骤，它看起来像这样：

1. 声明并将`count`初始化为 0。
2. 如果`count`小于 64，则继续步骤 3；否则，转到步骤 7。
3. 计算`bit`并显示它。
4. 移位掩码。
5. 将`count`增加 1。
6. 跳回第 2 行。
7. 在循环后继续执行程序。

`for`语句不需要其头部中的任何元素。表达式`for(; ;){ . . . }`完全有效；尽管仍然需要一种从循环中 thoát 的方式，以便它不会无限期地继续执行。（如果缺少条件，则假定为常量`true`。）

初始和循环表达式具有不寻常的语法，以支持需要多个循环变量的循环，如 Listing 3.46 所示。

#### LISTING 3.46: for Loop Using Multiple Expressions

```csharp
for (int x = 0, y = 5; ((x <= 5) && (y >= 0)); y--, x++)
{
    System.Console.Write(
        $"{ x }{{ ((x > y) ? '>' : '<') }}{ y }\t";
}
```

Listing 3.46 的结果出现在 Output 3.22 中。

#### OUTPUT 3.22

| 0<5 | 1<4 | 2<3 | 3>2 | 4>1 | 5>0 |

这里初始化子句包含一个复杂的声明，声明并初始化两个循环变量，但这至少类似于声明多个局部变量的声明语句。循环子句相当不寻常，因为它可以由逗号分隔的表达式列表组成，而不仅仅是一个表达式。

#### Guidelines

CONSIDER 如果发现自己编写具有复杂条件和多个循环变量的`for`循环，请重构该方法以使控制流更易于理解。

#### Guidelines

DO 当循环迭代次数事先已知并且循环中需要提供已执行迭代次数的“计数器”时，使用`for`循环。

DO 当循环迭代次数事先未知且不需要计数器时，使用`while`循环。

### The foreach Loop

C# 语言中的最后一个循环语句是 foreach。`foreach`循环遍历一组项目，将循环变量设置为依次表示每个项目。在循环体中，可以对该项目执行操作。`foreach`循环的一个优点是每个项目都恰好迭代一次；不可能像其他循环那样因计数错误而迭代超出集合末尾。

`foreach`语句的一般形式如下：

```
foreach(type variable in collection)
    statement
```

以下是`foreach`语句的分解：

- `type`用于声明集合中每个项目的变量的数据类型。它可以是`var`，在这种情况下，编译器从集合的类型推断出项目的类型。
- `variable`是一个只读变量，`foreach`循环将自动为其分配集合中的下一个项目。变量的作用域仅限于循环体。
- `collection`是一个表达式，例如数组，表示任意数量的项目。
- `statement`是循环体，在每次循环迭代时执行。

考虑在 Listing 3.47 所示的简单示例中`foreach`循环的上下文。
