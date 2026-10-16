
```csharp
{
    WriteLine("You typed in an empty string.");
}
else if (input.Length < 5)
{
    WriteLine("The string had less than 5 characters.");
}
else if (input.Length < 10)
{
    WriteLine("The string had at least 5 but less than 10 characters.");
}
WriteLine("The string was " + input);
}
```

你可以向一个 if 子句添加任意多个 else if，数量不限。

请注意，前面的示例声明了一个名为 `input` 的字符串变量，让用户在命令行输入文本，将其存入 `input`，然后测试该字符串变量的长度。这段代码还展示了在 C# 中进行字符串操作可以有多简单。例如，要获取 `input` 的长度，请使用 `input.Length`。

关于 if 语句，还有一点需要注意：当条件分支中只有一条语句时，不需要使用花括号：

```csharp
if (i == 0)
    WriteLine("i is Zero"); // This will only execute if i == 0
WriteLine("i can be anything"); // Will execute whatever the value of i
```

然而，为了保持一致性，许多程序员每次使用 if 语句时都倾向于使用花括号。

> **提示** if 语句不使用花括号可能会导致维护代码时出错。这种情况太常见了：在 if 语句中添加第二条语句，而无论 if 返回 true 还是 false，它都会执行。每次都使用花括号可以避免这种编码错误。
>
> 关于 if 语句的一个良好准则是：只有在语句与 if 语句写在同一行时，才允许程序员不使用花括号。有了这个准则，程序员就不太会在不添加花括号的情况下再添加第二条语句。

这里展示的 if 语句还说明了 C# 中一些用于比较值的运算符。特别是要注意，C# 使用 `==` 来比较变量是否相等。不要为此使用 `=`；单独的 `=` 用于赋值。

在 C# 中，if 子句中的表达式必须求值为布尔值。不能直接测试整数（例如，从函数返回的整数）。你必须将返回的整数转换为布尔值 `true` 或 `false`，例如，可以通过将该值与零或 `null` 进行比较：

```csharp
if (DoSomething() != 0)
{
    // Non-zero value returned
}
else
{
    // Returned zero
}
```

## `switch` 语句

`switch`/`case` 语句适合从一组互斥的执行分支中选择一个分支。它的形式是一个 `switch` 参数后跟一系列 `case` 子句。当 `switch` 参数中的表达式求值为某个 `case` 子句旁的值之一时，紧接该 `case` 子句之后的代码就会执行。这就是一个无需使用花括号将语句组成块的例子；相反，你要使用 `break` 语句来标记每个 case 代码的结束。你还可以在 `switch` 语句中包含一个 `default` 分支，如果表达式没有求值为其他任何分支的值，它就会执行。下面这个 `switch` 语句测试 `integerA` 变量的值：

```csharp
switch (integerA)
{
    case 1:
        WriteLine("integerA = 1");
        break;
    case 2:
        WriteLine("integerA = 2");
        break;
    case 3:
        WriteLine("integerA = 3");
        break;
    default:
        WriteLine("integerA is not 1, 2, or 3");
        break;
}
```

请注意，`case` 值必须是常量表达式；不允许使用变量。

尽管 C 和 C++ 程序员应该对 `switch`/`case` 语句很熟悉，但 C# 的 `switch`/`case` 比 C++ 的对应版本更安全一些。具体来说，它几乎在所有情况下都禁止贯穿（fall-through）行为。这意味着，如果某个 `case` 子句在块中较早触发，后面的子句就不能再触发，除非你使用 `goto` 语句表明你也希望它们触发。编译器会将每个未配备 `break` 语句的 `case` 子句都标记为错误，以此强制执行这一限制：

```text
Control cannot fall through from one case label ('case 2:') to another
```

虽然在少数情况下贯穿行为确实可取，但在绝大多数情况下，它都是无意的，并会导致难以发现的逻辑错误。为常规情况编写代码，而不是为例外情况编写代码，难道不是更好吗？

通过创造性地使用 `goto` 语句，你可以在 `switch` 分支中复现贯穿功能。然而，如果你发现自己真的很想这样做，那么你或许应该重新考虑你的方法。下面的代码既演示了如何使用 `goto` 模拟贯穿，也说明了最终代码可能会多么凌乱：

```csharp
// assume country and language are of type string
switch (country)
{
    case "America":
        CallAmericanOnlyMethod();
        goto case "Britain";
    case "France":
        language = "French";
        break;
    case "Britain":
        language = "English";
        break;
}
```

不过，禁止贯穿的规则有一个例外：如果某个 `case` 为空，你可以从一个 `case` 贯穿到下一个 `case`。这让你可以用相同的方式处理两个或多个 `case`（无需 `goto` 语句）：

```csharp
switch (country)
{
    case "au":
    case "uk":
    case "us":
        language = "English";
        break;
    case "at":
    case "de":
        language = "German";
        break;
}
```

关于 C# 的 `switch` 语句，一个有趣之处是 `case` 的顺序无关紧要——你甚至可以把 `default` 分支放在最前面！因此，不能有两个相同的 `case`。这包括具有相同值的不同常量，所以，例如你不能这样做：

```csharp
// assume country is of type string
const string england = "uk";
const string britain = "uk";
switch (country)
{
    case england:
    case britain:    // This will cause a compilation error.
        language = "English";
        break;
}
```

前面的代码还展示了 C# 的 `switch` 语句与 C++ 的另一个不同之处：在 C# 中，允许使用字符串作为被测试的变量。

## 循环

C# 提供了四种不同的循环（`for`、`while`、`do...while` 和 `foreach`），让你可以重复执行一段代码，直到满足某个条件。

### `for` 循环

C# 的 `for` 循环提供了一种循环迭代机制：在执行另一次迭代之前，先测试某个特定条件是否成立。语法如下：

```csharp
for (initializer; condition; iterator)
    statement(s)
```

其中：

- `initializer` 是在第一次循环执行之前求值的表达式（通常将局部变量初始化为循环计数器）。
- `condition` 是每次新的循环迭代之前检查的表达式（必须求值为 `true` 才会执行另一次迭代）。
- `iterator` 是每次迭代之后求值的表达式（通常递增循环计数器）。

当条件求值为 `false` 时，迭代结束。

`for` 循环是一种所谓的前测循环，因为循环条件是在执行循环语句之前求值的；因此，如果循环条件为 `false`，循环体根本不会执行。

`for` 循环非常适合按预定次数重复执行一条语句或一个语句块。下面的示例演示了 `for` 循环的典型用法。它会输出从 0 到 99 的所有整数：

```csharp
for (int i = 0; i < 100; i = i + 1)
{
    WriteLine(i);
}
```

在这里，你声明了一个名为 `i` 的 `int`，并将其初始化为零，它被用作循环计数器。然后立即测试它是否小于 100。由于该条件求值为 `true`，你执行循环中的代码，显示值 0。然后将计数器加 1，再重复这一过程。当 `i` 达到 100 时，循环结束。

实际上，前一个循环的写法并不是你通常的写法。C# 有一种给变量加 1 的简写形式，因此你可以直接写 `i++`，而不是 `i = i + 1`：

```csharp
for (int i = 0; i < 100; i++)
```
