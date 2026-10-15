
```
class TicTacToe        // Declares the TicTacToe class.
{
    static void Main()  // Declares the entry point of the program.
    {
        // Hardcode initial board as follows
        // ---------
        // 1 | 2 | 3
        // ---------
        // 4 | 5 | 6
        // ---------
        // 7 | 8 | 9
        // ---------
        char[] cells = {
            '1', '2', '3', '4', '5', '6', '7', '8', '9'
        };

        System.Console.Write(
            "The available moves are as follows: ");

        // Write out the initial available moves
        foreach (char cell in cells)
        {
            if (cell != 'O' && cell != 'X')
            {
                System.Console.Write($"{ cell } ");
            }
        }
    }
}
```

Output 3.23 显示了 Listing 3.47 的结果。

```
The available moves are as follows: 1 2 3 4 5 6 7 8 9
```

当执行引擎到达`foreach`语句时，它将变量`cell`分配给`cells`数组中的第一个项目——在本例中为值 1。然后，它执行构成`foreach`循环体的代码块中的代码。`if`语句判断`cell`的值是否为`'0'`或`'X'`。如果两者都不是，则将`cell`的值写入控制台。下一次迭代将下一个数组值赋给`cell`，依此类推。

请注意，编译器会防止在`foreach`循环执行期间修改变量（`cell`）。此外，循环变量在 C# 5 及更高版本中的行为与之前的版本略有不同；只有当循环体内包含使用该循环变量的 lambda 表达式或匿名方法时，这种差异才会显现。详见第 12 章。

## 初学者主题

### 何时更适合使用 switch 语句

有时你可能需要在多个连续的`if`语句中比较同一个值，如代码清单 3.48 中通过输入变量所示。

#### 代码清单 3.48：用 if 语句检查玩家的输入

```csharp
// ...

bool valid = false;

// Check the current player's input.
if ((input == "1") ||
    (input == "2") ||
    (input == "3") ||
    (input == "4") ||
    (input == "5") ||
    (input == "6") ||
    (input == "7") ||
    (input == "8") ||
    (input == "9"))
{
    // Save/move as the player directed.
    // ...

    valid = true;
}
else if ((input == "") || (input == "quit"))
{
    valid = true;
}
else
{
    System.Console.WriteLine(
        "\nERROR:  Enter a value from 1-9. "
        + "Push ENTER to quit");
}
// ...
```

这段代码验证输入的文本，以确保它是一次有效的井字棋走法。例如，如果`input`的值为 9，程序将不得不执行九次不同的求值。若能在一次求值后直接跳转到正确的代码，那会更好。为了实现这一点，可以使用`switch`语句。

## switch 语句

当一个值需要与许多不同的常量值进行比较时，`switch`语句比复杂的`if`语句更容易理解。`switch`语句如下所示：

```csharp
switch (expression)
{
    case constant:
        statements
    default:
        statements
}
```

下面是`switch`语句的详细说明：

- `expression` 是用于与不同常量进行比较的值。此表达式的类型决定了`switch`的“控制类型”。允许的控制数据类型有`bool`、`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、任意枚举类型（将在第 8 章介绍）、这些值类型各自对应的可空类型，以及`string`。

- `constant` 是与控制类型兼容的任何常量表达式。

- 一个或多个`case`标签（或`default`标签）后跟一个或多个语句的组合称为一个`switch`段。前面给出的模式包含两个`switch`段；代码清单 3.49 展示了一个包含三个`switch`段的`switch`语句。

- `statements` 是当表达式等于`switch`段中某个标签提到的常量值之一时要执行的一条或多条语句。该语句组的终点必须是不可达的。通常最后一条语句是一个跳转语句，如`break`、`return`或`goto`语句。

### 准则

> 不要使用`continue`作为退出`switch`段的跳转语句。当`switch`位于循环内部时，这样做是合法的，但很容易在后面某个`switch`段中对`break`的含义产生困惑。

`switch`语句至少应包含一个`switch`段；`switch(x){}`是合法的，但会产生一条警告。另外，之前的准则（见第 116 页）通常建议不要省略大括号。这条经验法则的一个例外是：对于`case`和`break`语句可以省略大括号，因为这些关键字本身就用于标识代码块的开始和结束，所以不需要大括号。

代码清单 3.49 中的`switch`语句在语义上等价于代码清单 3.48 中的一系列`if`语句。

### 代码清单 3.49：用 switch 语句替换 if 语句

```csharp
static bool ValidateAndMove(
    int[] playerPositions, int currentPlayer, string input)
{
    bool valid = false;

    // Check the current player's input.
    switch (input)
    {
        case "1":
        case "2":
        case "3":
        case "4":
        case "5":
        case "6":
        case "7":
        case "8":
        case "9":
            // Save/move as the player directed.
            ...
            valid = true;
            break;

        case "":
        case "quit":
            valid = true;
            break;

        default:
            // If none of the other case statements
            // is encountered then the text is invalid.
            System.Console.WriteLine(
                "\nERROR:  Enter a value from 1-9. "
                + "Push ENTER to quit");
            break;
    }

    return valid;
}
```

在代码清单 3.49 中，`input`是测试表达式。由于`input`是`string`类型，因此控制类型为`string`。如果`input`的值是字符串 1、2、3、4、5、6、7、8 或 9 之一，则该走法有效，并且你将相应的单元格更改为当前用户的棋子（X 或 O）。一旦执行遇到`break`语句，控制权就会离开`switch`语句。

下一个`switch`段描述了如何处理空字符串或字符串`quit`；如果`input`等于这两个值中的任何一个，它会将`valid`设置为`true`。如果没有其他`switch`段的`case`标签与测试表达式匹配，则执行`default` `switch`段。

### 语言对比：C++——switch 语句的贯穿

在 C++ 中，如果某个`switch`段没有以跳转语句结尾，控制流会“贯穿”到下一个`switch`段并执行其代码。由于意外贯穿是 C++ 中的常见错误，C# 不允许控制流从一个`switch`段意外地贯穿到下一个。C# 的设计者认为，与其模仿 C++ 那可能令人困惑的行为，不如预防这一常见的错误根源并鼓励更好的代码可读性。如果你确实希望一个`switch`段执行另一个`switch`段的语句，可以使用`goto`语句显式地实现，本章后面会演示。

关于`switch`语句，有几点需要注意：

- 没有`switch`段的`switch`语句会产生编译器警告，但语句仍能编译。

- `switch`段可以按任意顺序出现；`default`段不必放在最后。实际上，`default` `switch`段甚至可以不出现——它是可选的。

- C# 语言要求每个`switch`段的终点（包括最后一段）都必须是不可达的。这意味着`switch`段通常以`break`、`return`、`throw`或`goto`结尾。

## 跳转语句

可以改变循环的执行路径。实际上，使用跳转语句，可以跳出循环，或者跳过某次迭代的剩余部分并开始下一次迭代，即使循环条件仍然为真。本节将介绍一些将执行路径从一个位置跳转到另一个位置的方式。

### break 语句

为了跳出循环或`switch`语句，C# 使用`break`语句。只要遇到`break`语句，控制权就会立即离开循环或`switch`。代码清单 3.50 展示了井字棋程序中的`foreach`循环。

#### 代码清单 3.50：找到赢家后使用 break 跳出

```csharp
class TicTacToe    // Declares the TicTacToe class.
{
    static void Main() // Declares the entry point of the program.
    {
        int winner = 0;
        // Stores Locations each player has moved.
        int[] playerPositions = { 0, 0 };

        // Hardcoded board position.
        // X | 2 | O
        // --+---+--
        // O | O | 6
        // --+---+--
        // X | X | X
        playerPositions[0] = 449;
        playerPositions[1] = 28;

        // Determine if there is a winner.
        int[] winningMasks = {
            7, 56, 448, 73, 146, 292, 84, 273 };

        // Iterate through each winning mask to determine
        // if there is a winner.
        foreach (int mask in winningMasks)
        {
            if ((mask & playerPositions[0]) == mask)
            {
                winner = 1;
                break;
            }
            else if ((mask & playerPositions[1]) == mask)
            {
                winner = 2;
                break;
            }
        }

        System.Console.WriteLine(
            $"Player { winner } was the winner");
    }
}
```

#### 输出 3.24

```text
Player 1 was the winner
```

代码清单 3.50 在某个玩家占据获胜位置时使用了`break`语句。`break`语句会强制其所在的循环（或`switch`语句）停止执行，控制权转移到循环外的下一行。对于该清单，如果位比较返回`true`（即棋盘上有获胜位置），`break`语句会使控制权跳转并显示赢家。

## 初学者主题

### 位置判断的位运算符

井字棋示例（完整代码清单见附录 B）使用位运算符来确定哪一方赢得游戏。首先，代码将每个玩家的位置保存到一个名为`playerPositions`的位图中。（使用数组是为了能保存两个玩家的位置。）

首先，两个`playerPositions`均为 0。每当一个玩家走棋时，对应走棋的位被置为 1。例如，如果玩家选择单元格 3，`shifter`就被设为 3 - 1。代码减去 1 是因为 C# 从零开始索引，你需要将 0 而不是 1 作为第一个位置来调整。接下来，代码使用移位运算符`00000000000001 << shifter`设置`position`，即与单元格 3 对应的位，此时`shifter`的值为 2。最后，它将当前玩家的`playerPositions`（再次减去 1 以转换为从零开始）设置为`000000000000100`。清单 3.51 使用`|=`以便将之前的走棋与当前走棋合并。

#### 清单 3.51：设置与每位玩家走棋对应的位

```
int shifter; // The number of places to shift
// over to set a bit.
int position; // The bit that is to be set.

// int.Parse() converts "input" to an integer.
// "int.Parse(input) - 1" because arrays
// are zero based.
shifter = int.Parse(input) - 1;

// Shift mask of 00000000000000000000000000000001
// over by cellLocations.
position = 1 << shifter;

// Take the current player cells and OR them to set the
// new position as well.
// Since currentPlayer is either 1 or 2,
// subtract 1 to use currentPlayer as an
// index in a zero based array.
playerPositions[currentPlayer-1] |= position;
```

在程序稍后部分，你可以遍历棋盘上每个对应于获胜位置的掩码，以判断当前玩家是否处于获胜位置，如清单 3.50 所示。

## continue 语句

在循环中，你可能有一个包含一系列语句的代码块。如果确定在有些迭代中只需要执行这些语句的一部分，可以使用`continue`语句跳到当前迭代的末尾并开始下一次迭代。

`continue`语句退出当前迭代（无论是否还有其他语句）并跳到循环条件处。此时，如果循环条件仍然为真，循环将继续执行。

### 清单 3.52：确定电子邮件地址的域
