
第一条语句导致 `Visual Studio` 调用没有传递任何参数的构造函数。第三条语句导致 `Visual Studio` 调用接收了三个整数变量参数的构造函数。这引出了一个关于重载方法的重要规则：只要没有两个重载方法具有相同的签名，就可以对方法进行重载。这意味着只能有一个重载方法可以不传递任何参数。同样，只能有一个重载方法可以接收三个整数参数，但它们不能全都是整数。例如，你可以拥有一个具有以下签名的重载方法 `countThis()`：

```csharp
public int countThis(int val);
public int countThis(long val);
```

这些是完全可以的，因为它们的签名不同；因此，两种形式都接受一个参数，但参数的数据类型不同；签名是不同的。如果你滚动查看 `DateTime` 数据类型的 12 个构造函数，你会发现所有 12 种不同的参数都曾传递给它们。

当你需要编写在传递不同信息时具有不同行为的方法时，重载方法非常有用。你可以在后面的章节中看到重载方法的其他示例。

# 刷新按钮

在“最后尝试”中，刷新按钮的目的是更新任何使用时间组件的字符串的时间部分。代码如下：

```csharp
private void btnRefresh_Click(object sender, EventArgs e)
{
    UpdateTimeInfo();
}
```

当用户点击刷新按钮 `btnRefresh` 时，代码调用 `UpdateTimeInfo` 方法来更新文本框中的信息。注意，你在程序的两个不同位置调用了 `UpdateTimeInfo` 方法：一次在 `frmMain()` 构造函数中，另一次在 `btnRefresh_Click()` 方法中。

你可以调用方法，这说明了方法的另一个重要特性：它们让你能够避免重复代码。你可以随后将以下代码复制并显示在 `frmMain()` 构造函数和 `btnRefresh_Click()` 方法中：

```csharp
int days;
DateTime myTime = new DateTime();
myTime = DateTime.Now;
DateTime years = new DateTime(myTime.Year, 12, 31);
xtDateTimeAndTime.Text = myTime.ToString("f");
xtLongDate.Text = myTime.ToString("D");
xtShortDate.Text = myTime.ToString("d");
xtGeneralAndTime.Text = myTime.ToString("g");
xtLongTime.Text = myTime.ToString("T");
xtShortTime.Text = myTime.ToString("t");

days = years.DayOfYear;
xtDaysToNewYears.Text = days.ToString();
```

但如果你这样做，你就有两倍的代码需要编写和维护。通过将代码放在方法中。

观察者。然而，经验告诉我，程序开发的 80% 时间都花在了测试、调试和维护代码上，而只有 20% 花在编写代码。因此，任何可以让你的代码更清晰、更易理解的办法都是好主意。

## 关系运算符

对任何事情做出决定都涉及到将一个与另一个进行比较。计算机程序中也是如此。你在第 3 章中已经了解到，语句是由运算符和操作数构建的。你曾使用数学运算符来说明程序语句是如何从这些基本单元构建而成的。在本节中，你将学习另一组你可以运的运算符：关系运算符。关系运算符如表 6-1 所示。

表 6-1：关系运算符

| 关系运算符 | 关系测试 | 示例 | 结果 |
| --- | --- | --- | --- |
| `==` | 等于 | `15 == 20` | false |
| `!=` | 不等于 | `15 != 20` | true |
| `<` | 小于 | `15 < 20` | true |
| `<=` | 小于或等于 | `15 <= 20` | true |
| `>` | 大于 | `15 > 20` | false |
| `>=` | 大于或等于 | `15 >= 20` | false |

参考表 6-1，每个示例在关系运算符的左侧有一个操作数 `15`，在关系运算符的右侧有第二个操作数 `20`。当两个操作数与关系运算符相关时，所有的关系运算符都是二元运算符。因此，使用关系运算符结合两个操作数会得到一个关系表达式。

每个关系表达式最终解析为逻辑 True 或 false。在 C# 中，逻辑解析为 C 关键字 `true` 或 `false`。参考表 6-1，第三列所示的每个示例都解析为第四列所示的状态。使用这些值仅是为了使关系表达式更具体。在编程场景中，关系表达式中的操作数通常是变量而不是字面量。

## 使用关系运算符——if 语句

现在考虑你学到的关系运算符，并将它们应用于 C# 的 `if` 语句中。虽然你在前面的章节中已经见过几个 `if` 语句的示例，但还没有解释它们的工作原理。这就是本节的目的。

`if` 语句的语法如下：

```csharp
if (expression1)
{
// Logic true: if 语句块
}
```

`expression1` 出现在 `if` 关键字后的左括号和右括号之间。通常，`expression1` 代表要执行的关系测试。参考表 6-1，关系表达式的结果是逻辑 True 或 False。出现在大括号之间的代码是 `if` 语句块。如果 `expression1` 结果为逻辑 True，则执行该语句块。如果 `expression1` 结果为逻辑 False，程序控制将跳过 `if` 语句块，并在 `if` 语句块大括号之后的下一个语句处继续执行程序。你可以从图 6-1 查看程序是如何根据 `expression1` 的结果流动的。

让我们通过一个简单的程序来判断数字是奇数还是偶数，测试你对 `if` 语句工作工作的理解。

![](img/4329bd7a4f8df07f46abc710b6d0939f_182_0.png)

图 6-1：if 语句块

## 测试奇偶数 `Chapter06ProgramOddEven`

为了说明 `if` 语句的简单用法，请图 6-2 所示的程序。

1. 在第 2 章中使用 C# 模板创建一个新项目。
2. 添加两个标签对象、一个文本框对象两个按钮。
3. 按照你的要求设置对象的属性。图 6-2 是你可能使用的用户界面示例。
4. 添加按钮点击事件代码，如代码 6-1 所示。

![](img/4329bd7a4f8df07f46abc710b6d0939f_182_1.png)

图 6-2：奇偶数程序

用户输入一个数字，程序根据其值告诉他们该数字是奇数还是偶数。字母 O 就在数字字符 `0` 下方，有时人们匆会按错键。

### 代码 6-1：`btn-Click` 事件代码 `frmMain.cs`

```csharp
private void btnCac_Calc_Click(object sender, EventArgs e)
{
    bool flag;
    int val;
    string output = "Number is even";

    // 从文本转换为数字
    flag = int.TryParse(txtNumber.Text, out val);
    if (flag == false)
    {
        MessageBox.Show("Not a number. Re-enter.");
        txtNumber.Clear();
        txtNumber.Focus();
        return;
    }
    // 查看奇奇偶
    if (val % 2 == 1)
    {
        output = "Number is odd";
    }
    // 显示结果
    lblOutput.Text = output;
}
```

工作原理

执行所有工作的代码都在点击事件中 `参考代码 6-1`。

理解语句如何改变程序流程的最佳方法，是使用 `var` 的不同值对代码进行单步执行。要做到这一点，请将光标置在以下语句上：

```
flag = int.TryParse(txtName.Text, out val);
```

然后按 `F9` 键开始设置调试断点。现在运行程序。当程序到达断点时，通过反复按 `F10` 键对程序进行单步执行。`你也可以使用 F11` 键，甚至更好，因为会让程序在进入你编写的任何方法时也进行单步执行。

## “使用了未赋值的局部变量”

有时，当你使用该语句时，可能会遇到以下错误消息：

```
use of unassigned local variable i
```

你可以通过以下代码段来演示这一点：

```
int i;
// 一些额外的代码行
if (x == MAX)
{
    i = 10;
}
i *= i;
```

`Visual Studio` 对最后一行程序代码发布错误消息，指出你正尝试在给变量赋值之前使用它。`Visual Studio` 之所以这样做，是因为它无法编译语句是否返回逻辑 True 来将值 10 赋值给 `i`。如果表达式逻辑为 False，变量 `i` 就是未初始化的，并且没有已知的赋值值。你可以简单地用默认值初始化变量 `i` 来解决这个问题。大多数情况下，你会在定义变量时完成这一点。只需将 `i` 的定义更改如下所示：

```
int i = 0;
```

这会将 `i` 的右值设置为 0，`Visual Studio` 就很满意了，因为无论 `if` 表达式的结果如何，`i` 现在都有了一个已知的值。

### if-else 语句

如果你仔细观察列表 6-1 中的代码，你会注意到即使在定义字符串时，输出字符串也被设置为字面量 `Number is even`。因此，字符串只有在数字为奇数时才会改变。如果你想一下，你实际上想做的是根据数字是奇是偶设置输出字符串。程序可以工作，但它并没有反映你的真实意图。

`if-else` 语句是清晰代码的完美解决方案。`if-else` 语句的语法如下：

```
if (expression1)
{
// 逻辑为真：if 语句块
}
else{
    // 逻辑为假：else 语句块
}
```

使用 `if-else` 语句，如果 `if (expression1)` 为真，则执行 `if` 语句块。如果 `expression1` 为假，则执行 `else` 关键字之后的大括号内的语句。`else` 关键字之后大括号内的语句组被称为 `else` 块。`if-else` 语句的程序流如图 6-3 所示。

![](img/4329bd7a4f8df07f46abc710b6d0939f_186_0.png)

正如图 6-3 所示，`if-else` 语句创建了一种“非此即彼”的决策。也就是说，该决策会产生互斥的结果之一。在接下来的尝试中，你将修改 6-1 所示的程序使用 `if-else`

图 6-3：`if-else` 语句块

## 尝试 if-else 语句 `Chapter06ProgramOddEven.zip`

为了演示 `if-else` 语句块的一些用法，请修改图 6-2 所示的程序。

- 1. 加载你在本章节早期编写的简单 `if` 的程序。
- 2. 将 `output` 的定义更改为：`string output;`
- 3. 将第二个语句替换为：

```
// 检查是奇数还是偶数
if (val % 2 == 1)
{
output = "Number is odd";
else{
output = "Number is even";
}
```

### 工作原理

大多数程序员都会同意，这种形式易于理解，因为结果是清晰陈述的。在简单的 `if-else` 形式中，你不需要换行和缩进就能看到结果。大多数程序员会认为这种形式更易于理解，因为结果是清晰陈述的。在简单的 `if-else` 形式中，你不需要换行和缩进就能看到结果。大多数程序员会认为这种形式更易于理解，因为结果是清晰陈述的。述的，在简单的 `if-else` 语句中，你不需要换行和缩进就能看到结果。这种形式更易于理解，因为结果是清晰陈述的。在简单的 `if-else` 语句中，你不需要换行和缩进就能看到结果。大多数程序员会认为这种形式更易于理解，因为结果是清晰陈述的。在简单的 `if-else` 语句中，你不需要换行和缩进就能看到结果。大多数程序员会认为这种形式更易于理解，因为结果是清晰陈述的。在简单的 `if-else` 语句中，你不需要换行和缩进就能看到结果。

## if-else 的简写形式：三元运算符

由于 `if-else` 语句非常常见，C# 有一种专门设计的特殊运算符来替换它们。三元运算符的语法是替换简单的 `if-else` 语句：

```
(expression1) ? trueExpression : falseExpression
```

三元运算符的工作方式是首先评估 `expression1`。如果 `expression1` 为真，则执行 `trueExpression`。如果 `expression1` 为假，则执行 `falseExpression`。逻辑流如图 6-4 所示。

![](img/4329bd7a4f8df07f46abc710b6d0939f_187_0.png)

图 6-4：`if-else` 语句

在接下来的尝试中，你使用修改 6-1 所示的程序使用三元运算符。

尝试三元运算符 `Chapter06ProgramOddEven.zip`

为了演示三元运算符的一些用法，请修改图 6-2 所示的程序。

- 1. 加载你在本章节早期编写的简单 `if` 的程序。
- 2. 将 `output` 的定义更改为：`string output;`
- 3. 将 `if-else` 语句替换为：

```
// 检查是奇数还是偶数
output = (val % 2 == 1) ? "Number is odd" : "Number is even";
```

如果 `val % 2 == 1` 为真，`output` 被赋值为 `"Number is odd"`；否则，取模运算符产生 1，`output` 被赋值为 `"Number is even"`。现在运行程序查看它是否如之前一样运行。

### 工作原理

尽管三元运算符是 `if-else` 语句的简写，但我并不喜欢它的用法。有三个原因。首先，大多数程序员理解三元表达式比理解 `if-else` 语句花费更多时间。其次，我有一种挥不去的直觉，使用它的人是为了能用它。第三，如果我在读完三元语句后，感觉程序员在说：“看好了，Billy-Bob。”考虑到这些原因，如果使用简单的 `if-else` 语句代码更清晰，请使用 `if-else`。

## if 和 if-else 语句的样式考量

C# 是一种对格式无关的语言。这意味着你可以将 `if-else` 语句写为单行，例如：

```
if (val % 2 == 1) (output = "Number is odd";output = "Number is even");
```

`Visual Studio` 可以正常处理这些语句。然而，大多数程序员会认为没有换行和缩进的前一行更难以阅读。这种格式问题属于你编写代码时的样式问题。

例如，当 `if` 或 `else` 块只包含一条语句时，就不需要大括号。也就是说，你可以将以下代码：

```
if (val % 2 == 1)
{
    output = "Number is odd";
else
{
    output = "Number is even";
}
```

写成这样：

```
if (val % 2 == 1)
    output = "Number is odd";
else
    output = "Number is even";
```

程序的执行结果与之前完全相同。然而，当 `if` 语句包含多条语句时，你必须使用大括号。假设你写了以下代码：

```
if (val % 2 == 1)
{
```

```cs
output = "Number is odd";
oddCounter++;
```

你的意图是使用 `oddCounter` 统计奇数的个数。如果你在不使用括号的情况下编写相同的代码：

```cs
if (val % 2 == 1)
    output = "Number is odd";
    oddCounter++;
```

你的意图可能是一样的，但如果没有大括号，你实际得到的是：：

```cs
if (val % 2 == 1)
{
    output = "Number is odd";
}
oddCounter++;
```

代码之所以不同，是因为在没有大括号的情况下，`if` 语句只控制一条语句。结果是无论 `val` 的值如何，`oddCounter` 都会增加——这可能不是你想要的。

因此风格问题变成了：“当 `if` 语句块只包含一条语句时，你应该使用大括号吗？”答案是肯定的。始终使用大括号。首先，它促进了代码的一致性。每当你使用 `if` 语句时，都会紧跟大括号。其次，原本 `if` 语句块中的单条语句在经过测试和调试后可能会变成多条语句。你迟早需要添加大括号，不如从一开始就加上。第三，大多数程序员认为大括号让语句块更加突出，更易于阅读。在这里学到的教训是，即使 `if` 语句块只包含一条语句，也要始终使用大括号。

另一个风格考量是大括号的位置。例如，由于 C# 不在乎语句的格式，你可以这样写代码：

```cs
if (val % 2 == 1)
    output = "Number is odd";
else
    output = "Number is even";
```

注意，必需的大括号仍然位于它们该在的位置，但位置有所不同。这种 K&R 风格因 Brian Kernighan 和 Dennis Ritchie 编写的 C 语言书籍 `The C Programming Language`, `Prentice Hall`, `1978` 而流行。采用这种风格的原因之一是它占用的屏幕行较少，这意味着你可以更好地利用显示器的微小区域。无需滚动即可看到更多代码是一件好事。
